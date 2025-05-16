---
sidebar_position: 4
---

Allows a Class (or any table with __index with cyclic reference) to inheritMethods and behavior from parent class that supports inheritence.
:::note
This only inherits the behavior, the created objects will not get the inherited behavior by default, you must use superClass function to get the inherited behavior and fields.
:::

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

local inheritClass = require(Modules.Functions.inheritClass)

-- [Class Definition] --
local MyClass = {}
inheritClass(MyClass, Modules.Classes.Class, "MyClass") -- Inherits the behavior

return MyClass
```