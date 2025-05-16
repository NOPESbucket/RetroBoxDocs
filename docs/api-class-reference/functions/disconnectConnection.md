---
sidebar_position: 3
---

Disconnects a [RBXScriptConnection](https://create.roblox.com/docs/reference/engine/datatypes/RBXScriptConnection). The passed connection can be a nil value allowing to put this function in a code where you may not always have a [RBXScriptConnection](https://create.roblox.com/docs/reference/engine/datatypes/RBXScriptConnection) present.
```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Functions] --
local disconnectConnection = require(Modules.Functions.disconnectConnection)

local playerConnection = game.Players.LocalPlayer.CharacterAdded:Connect(function()
    print("Character Respawned")
end)
disconnectConnection(playerConnection) -- Will disconnect the connection
disconnectConnection(nil) -- Will do nothing if nil is passed making this function nil safe
```