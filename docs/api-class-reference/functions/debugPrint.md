---
sidebar_position: 2
---

Prints a debug message if provided script has attribute `Debug` set to true.
The following message will output when using this function.

```lua title="ServerScriptService/Server.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Functions] --
local debugPrint = require(Modules.Functions.debugPrint)

debugPrint(script, "Hello World!") -- Outputs: [Server]: Hello World!
```