---
sidebar_position: 1
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

Class - is a **base class** which serves as the foundation for all of the other classes that want inheritence support.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

local inheritClass = require(Modules.Functions.inheritClass)
local superClass = require(Modules.Functions.superClass)

-- [Class Definition] --
local MyClass = {}
inheritClass(MyClass, Modules.Classes.Class, "MyClass")

function MyClass.new()
    local self = setmetatable({}, MyClass)
    superClass(self, MyClass)
    return self
end

function MyClass.Destroy(self)
    if table.isfrozen(self) then
        return
    end

    table.clear(self)
    table.freeze(self)
end

return table.freeze({
    new = MyClass.new
})
```

## Properties
---
### > `ClassData: number | 1` <Tag color="#e3ce8b">Public</Tag>

A dummy property.

---
### > `_Inherited: any` <Tag color="#4958df">Private</Tag>

This property is used for look ups of the inherited data. **Don't access it**, this is used by `metamethods`!

## Constructor
---
### > `Class.new(...any)`

## Methods
---
### > `Class:IsA(className: string): boolean` <Tag color="#e3ce8b">Public</Tag>
Checks whether class is the specfic class type.

---
### > `Class:Destroy(): boolean` <Tag color="#e3ce8b">Public</Tag>
Destroy's class and releases itself from the memory.
:::info
This is just an **Interface**, you still have to implement clean up mechanism.
:::