---
sidebar_position: 11
---

Promise - implementation of JavaScript Promise.

---
## Why use Promises?
---

Before diving in to Promises themselves, you might need some convincing of why we should even use Promises to begin with. That's totally fair! The following text should give you a brief introduction to Promises and a good understanding of why they are useful.

---
## Threads​
---

When writing programs, it's possible to divide functions into two groups: "synchronous" and "asynchronous". A "synchronous operation" is one that can run to completion and generate any necessary return values with only the information available to your code at the time the operation begins. For example, a function that takes two Parts and returns the distance between them would be synchronous, because all information needed to compute that value is available when you call the function.

But sometimes situations arise where we call a function that needs access to a value that doesn't exist at call time. This could be because it requires a network request to get the data, or the user needs to input some text, or we're waiting for another process to finish computation and give us the value. In any case, we refer to this as an "asynchronous operation".

The simplest way to deal with this is to just stop execution of the thread, or "block". This means that when you call a function that needs some data that doesn't exist yet, the entire thread stops running and waits for the data to be ready before returning and continuing. This is actually how many low-level languages typically model asynchronous operations. To allow tasks to run at the same time, programs will create new threads that branch from parent threads and jump back on when they're finished blocking. However, this presents challenges with sharing memory and synchronizing data across threads, because at the operating system level threads truly are running in parallel.

---
## Coroutines​
---

To simplify sharing memory and potentially reduce overhead, many programs will emulate a multi-threaded environment using green threads or coroutines, which are run concurrently inside of one OS thread. The key difference between OS threads and coroutines is that coroutines do not actually run in parallel -- only one coroutine is ever executing at a time. In the context of Lua, the term "thread" is used to refer to a coroutine, but they are not the same thing as OS threads.

To facilitate this emulation, a thread scheduler is introduced to keep track of the emulated threads and decide which thread to run next when the current thread yields. Yielding is similar to blocking, except when a coroutine yields, it signals to the thread scheduler that it can run other code and resume the thread at a later time.

When the game starts, each Script and LocalScript in your game becomes its own Lua thread in the thread scheduler and each script is run either to completion or until it yields. Once all of the scripts have gone through this process, Roblox does other things like updating humanoids and running physics. After all that's done, the next frame begins and this process repeats until the game closes.

So, what really happens when we call an asynchronous function like `Player:IsInGroup`? Well, the current Lua thread yields (letting other Lua code start running elsewhere in your game), and Roblox makes a new OS thread which blocks on an HTTP request to their internal group APIs in the background. Sometime in the future when that request comes back, the value jumps back onto the main Roblox thread and your Lua thread is scheduled to be resumed with the given arguments on the next step.

Problems with the Coroutine Model​
Coroutines fix the memory sharing problem of OS threads, but they still inherit other problems when used on their own:

It's impossible to know if a function that you call is going to yield or not unless you look at the documentation or strictly abide by a naming convention (which is not realistic). Unintentionally yielding the thread is the source of a large class of bugs and race conditions that Roblox developers run into.
When an asynchronous operation fails or an error is encountered, Lua functions usually either raise an error or return a success value followed by the actual value. Both of these methods lead to repeating the same tired patterns many times over for checking if the operation was successful, and make composing multiple asynchronous operations difficult.
It is difficult to deal with running multiple asynchronous operations concurrently and then retrieve all of their values at the end without extraneous machinery.
Coroutines lack easy access to introspection without manual work to enable it at the call site.
Coroutines lack the ability to cancel an operation if the value is no longer needed without extraneous manual work at both the call site and the function implementation.
Enter Promises​
In Lua, Promises are an abstraction over coroutines. A "Promise" is just an object which we can use to represent a value that exists in the future, but doesn't right now. Promises are first-class citizens in other languages like JavaScript, which doesn't have coroutines and facilitates all asynchronous code through callbacks alone.

When calling an asynchronous function, instead of yielding, the function returns a Promise synchronously. The Promise object allows you to then attach a callback function which will be run later when the Promise resolves. The function you called is in charge of resolving the Promise with your value when it is done working.

Promises also have built-in error handling. In addition to resolving, a Promise can reject, which means that something went wrong when getting the future value we asked for. You can attach a different callback to be run when the Promise rejects so you can handle any error cases.

Let's take a look at this in action. We will make a function which wraps `HttpService:GetAsync` and instead of yielding, it will return a Promise.

Full documentation [here](https://eryn.io/roblox-lua-promise/docs/intro).