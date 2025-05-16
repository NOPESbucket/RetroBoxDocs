---
sidebar_position: 11
---

`Author: Sleitnick`

Signal - is a Signal class which has effectively identical behavior to a normal `RBXScriptSignal`, 
with the only difference being a couple extra stack frames at the bottom of the stack trace when an error is thrown.
This implementation caches runner coroutines, so the ability to yield in the signal handlers comes at minimal extra cost over a naive signal 
implementation that either always or never spawns a thread.

Full documentation [here](https://sleitnick.github.io/RbxUtil/api/Signal/).