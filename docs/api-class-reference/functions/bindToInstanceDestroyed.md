---
sidebar_position: 1
---

When using Deferred signal mode: scripts parented to an object cannot listen to that object's Destroying event, since it is disconnected up before being executed.
To avoid this, we'll use a hacky solution and clone a listener script into PlayerScripts.
This script will continue running after the instance is destroyed and allow us to run e.g. cleanup code when it gets destroyed.

```lua title="Workspace/Model/ModelScript.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Functions] --
local debugPrint = require(Modules.Functions.debugPrint)

-- [Instances] --
local model = script.Parent

-- This will not run in Deffered mode, because script will be deleted before the Destroying event will be executed
model.Destroying:Connect(function()
    print("Destroying callback")
end)

-- This will run no matter
bindToInstanceDestroyed(model, function()
    print("bindToInstanceDestroye callback")
end)

model:Destroy()
```