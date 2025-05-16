---
sidebar_position: 12
---

export const Tag = ({children, color}) => (
    <span style={{
            fontSize: '0.75em', 
            backgroundColor: color,
            borderRadius: '4px',
            color: '#fff',
            padding: '0.2rem 0.5rem',
            fontWeight: 'bold',
        }}>
    {children}
    </span>
)

Stack - is a linear data structure with a collection of items that follows the Last-In-First-Out (LIFO) principle. The top of the stack is the item most recently added to the stack, and the bottom of the stack is the item that was least recently added.\
You can think of the stack data structure as a stack of dinner plates: you start with one, and then you put another above it. When you take plates from the stack, the first one you remove from the stack is the last one you put on the top.\
Stacks have two main operations: push for adding an element to the top of the stack and pop for removing the element from the top of the stack. A Stack can either have a fixed size or be dynamically resized. Stacks are helpful for design usage such as backtracking algorithms.

![stack-visual](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.I9ag8MpibXiJFGz7SdT_eQHaEK%26pid%3DApi&f=1&ipt=7b6ddae124e83c56644799be35f823f11f6ae6b0b27f5caf0afafa1c26246e8c&ipo=images)

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Stack = require(Modules.Utility.Stack)

-- [Objects] --
local s = Stack.new()

-- Change the stack 	Resulting stack		 Output

s:Push(1)      			-- {1}

s:Push(5)      			-- {1, 5}

s:Push(10)     			-- {1, 5, 10}

print(s:Pop()) 			-- {1, 5}            10

print(s:Pop()) 			-- {1}               5

s:Push(20)     			-- {1, 20}

print(s:Pop()) 			-- {1}               20

print(s:Pop()) 			-- {}                1
```

## Properties
---

### > `_data: {any}` <Tag color="#4958df">Private</Tag>
An array of values that are in the stack.

## Methods

---
### > `Stack:Push(Element: any)` <Tag color="#e3ce8b">Public</Tag>
Pushes the element to the stack.

---
### > `Stack:Pop(): any` <Tag color="#e3ce8b">Public</Tag>
Pops the element to the stack.

---
### > `Stack:Peek(): any` <Tag color="#e3ce8b">Public</Tag>
Returns last element in the stack.

---
### > `Stack:Empty(): boolean` <Tag color="#e3ce8b">Public</Tag>
Checks whether stack is empty or not.

---
### > `Stack:Search(Element: any): number` <Tag color="#e3ce8b">Public</Tag>
Searches element inside stack. Returns position of the element in the stack. If -1 is returned, that means element is not present in the stack.

---
### > `Stack:__tostring(): string` <Tag color="#4958df">Private</Tag> <Tag color="#E6AF59">Metamethod</Tag>
Returns the string representation of the stack. Use tostring(myStack) to get the string representation of a stack.

---
### > `Stack:__iter(): (typeof(next), {any})` <Tag color="#4958df">Private</Tag> <Tag color="#E6AF59">Metamethod</Tag>
Returns the iterator for the stack object.
```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Stack = require(Modules.Utility.Stack)

-- [Objects] --
local myStack = Stack.new()

myStack:Push(1)
myStack:Push(2)
myStack:Push(3)

for i, element in myStack do
    print(i, element)
end
-- Output: 1
-- Output: 2
-- Output: 3
```

---