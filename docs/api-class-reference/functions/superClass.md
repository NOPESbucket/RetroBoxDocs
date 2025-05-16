---
sidebar_position: 5
---

*Adds or supers* the behaviors from the inherited Class table to the created object.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

local inheritClass = require(Modules.Functions.inheritClass)

-- [Class Definition] --
local MyClass = {}
inheritClass(MyClass, Modules.Classes.Class, "MyClass") -- Inherits the behavior

function MyClass.new()
    local self = setmetatable({}, MyClass)
    superClass(self, MyClass) -- Supers the behavior allowing us to call parent methods
    return self
end

return MyClass
```