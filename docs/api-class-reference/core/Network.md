---
sidebar_position: 2
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

Network - is a network abstraction layer for [Warp](https://imezx.github.io/Warp/) that works both `Server/Client`. This can be inherited allowing you to easily do *RPC calls*.

## Constructor

---
### > `Network.new(): Types.Network` <Tag color="#e3ce8b">Public</Tag>
Creates a new Network object that allows Server/Client communication.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)
local Remotes = require(script.Remotes)

local network = Network.new() -- Create new Network object
for k, v in Remotes do
	if type(v) ~= "string" then
		continue
	end
	network:CreateRemote(v, Remotes.SetupRemotes[k]) -- Create new Remote communication bridge
end
network:Destroy() -- Destroy it (note: Remotes that were created are persistent)
```

## Methods

---
### > `Network.CreateRemote(self: Types.Network, remoteName: string, conf: any?): ()` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag> <Tag color="#70E860">Client</Tag>
Creates a new Remote communication bridge.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

network:CreateRemote("Egg") -- Create "Egg" Remote
```

---
### > `Network.ConnectRemote(self: Types.Network, remoteName: string, callback: (...any) -> ()): string` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag> <Tag color="#70E860">Client</Tag>
Connects a function callback to a specified remote.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

-- Connect to a "Egg" Remote (note: Remote must exists prior to trying connecting function callback to it)
network:ConnectRemote("Egg", function(name)
    print("My name is:", name)
end)
```

---
### > `Network.ConvertConnectionLike(self: Types.Network, remoteName: string, key: string): Types.ConnectionLike` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag> <Tag color="#70E860">Client</Tag>
Converts a connection ID to a ConnectionLike Object. This is usefull for automatic memory clean up when `:Destroy()` method is called.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)
local Trove = require(Modules.Utility.Trove)

-- [Objects] --
local network = Network.new()
local trove = Trove.new()

-- Add the connection to trove
trove:Add(network:ConvertConnectionLike("Egg", network:ConnectRemote("Egg", function(name)
    print("My name is:", name)
end)))
trove:Destroy() -- Destroying trove will disconnect the Remote connection which will release memory
```

---
### > `Network.DisconnectRemote(self: Types.Network, remoteName: string, key: string): ()` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag> <Tag color="#70E860">Client</Tag>
Disconnects a function callback from a remote with specified connection ID.

```lua
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

-- connection variable will store our ID connection
local connection = network:ConnectRemote("Egg", function(isEgg: boolean) -- Assuming you have the "Egg" remote already
    print("IsEgg", isEgg)
end)

network:DisconnectRemote("Egg", connection) -- Effectively disconnects a function callback from the remote
```

---
### > `Network.FireRemote(self: Types.Network, remoteName: string, reliable: boolean, player: Player | nil, ...: any): ()` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag> <Tag color="#70E860">Client</Tag>
Sends data to a specified remote to a specific [player](https://create.roblox.com/docs/reference/engine/classes/Player) or server. \

:::note
Data will be compressed to reduce latency, but buffer objects can't be passed.
:::

```lua title="ServerScriptService/Server.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

network:ConnectRemote("Egg", function(isEgg: boolean)
    print("IsEgg", isEgg)
end)
```

```lua title="StarterPlayer/StarterPlayerScripts/Client.client.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

while task.wait(1) do
    network:FireRemote("Egg", true, nil, math.random() > 0.5) -- On client side we can't pass a Player to FireRemote() so we have to use nil
end
```

---
### > `Network.FiresRemote(self: Types.Network, remoteName: string, reliable: boolean, ...: any): ()` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag>
Sends data to all [players](https://create.roblox.com/docs/reference/engine/classes/Player) on the server.

```lua title="ServerScriptService/Server.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

network:FiresRemote("Egg", true, "I'm the Egg!")
```

---
### > `Network.FireExceptRemote(self: Types.Network, remoteName: string, reliable: boolean, except: {Player}, ...: any): ()` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag>
Sends data to all players, but filters out certain players if they are in the `except` filer.

```lua title="ServerScriptService/Server.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Services] --
local Players = game:GetService("Players")

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

network:FireRemoteExcept("Egg", true, { Players:GetPlayers()[math.random(1, #Players:GetPlayers())] } "I'm the Egg!") -- A random player will not receive this message
```

---
### > `Network.Invoke(self: Types.Network, remoteName: string, timeout: number, player: Player, ...: any): (...any)` <Tag color="#e3ce8b">Public</Tag> <Tag color="#2596be">Server</Tag>
Invokes Server/Client waiting for it to return a value

:::warning
This method Yields!
:::

```lua title="ServerScriptService/Server.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

local player = Players:GetPlayers()[math.random(1, #Players:GetPlayers())]
local result = network:Invoke("Egg", 60, player) -- Thread will yield here
print("IsEgg", result)
```

```lua title="StarterPlayer/StarterPlayerScripts/Client.client.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local Network = require(Modules.Classes.Network)

-- [Objects] --
local network = Network.new()

network:CreateRemote("Egg") -- You must declare "Egg" remote both on server/client

network:ConnectRemote("Egg", function()
    return math.random() > 0.5
end)
```

---
### > `Network.Destroy(self: Types.Network): ()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Network object releasing it from memory.
:::info
Remotes that were created in the network objects lifespan are persistant.
:::