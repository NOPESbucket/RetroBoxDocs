---
sidebar_position: 11
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

Queue - is a collection of entities that are maintained in a sequence and can be modified by the addition of entities at one end of the sequence and the removal of entities from the other end of the sequence. By convention, the end of the sequence at which elements are added is called the back, tail, or rear of the queue, and the end at which elements are removed is called the head or front of the queue, analogously to the words used when people line up to wait for goods or services.

![queue-visual2](https://prod.docsiteassets.roblox.com/assets/data/memory-store/Priority-Queue-Diagram.png.webp)

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Queue = require(Modules.Utility.Queue)

-- [Objects] --
local myQueue = Queue.new()

-- Add some values to the queue
myQueue:Enqueue(5)
myQueue:Enqueue(10)
myQueue:Enqueue(15)

-- myQueue = { 5, 10, 15 }

-- Remove one value from the queue
local first = myQueue:Dequeue()
print("The first value added to the queue was", first)

-- myQueue = { 10, 15 }

-- Add more values to the queue
myQueue:Enqueue(20)
myQueue:Enqueue(25)
myQueue:Enqueue(30)

-- myQueue = { 10, 15, 20, 25, 30 }

-- Remove another value from the queue
local second = myQueue:Dequeue()
print("The second value added to the queue was", second)

-- myQueue = { 15, 20, 25, 30 }
```

## Properties
---
### > `_first: number` <Tag color="#4958df">Private</Tag>
---
### > `_last: number` <Tag color="#4958df">Private</Tag>
---
### > `_queue: { T }` <Tag color="#4958df">Private</Tag>
---

## Methods
---

### > `Queue:IsEmpty(): boolean` <Tag color="#e3ce8b">Public</Tag>
Checks whether the queue is empty.

---
### > `Queue:Enqueue(value: T)` <Tag color="#e3ce8b">Public</Tag>
Adds value to a queue.

---
### > `Queue:Dequeue(): T` <Tag color="#e3ce8b">Public</Tag>
Removes a value from the queue.

---
### > `Queue:GetQueueLenght(): number` <Tag color="#e3ce8b">Public</Tag>
Returns current lenght of the queue.

---
### > `Queue:IsInQueue(item: any): boolean` <Tag color="#e3ce8b">Public</Tag>
Check whether item is in queue or not.

---
### > `Queue:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's and clears the Queue, releasing it from memory.

---