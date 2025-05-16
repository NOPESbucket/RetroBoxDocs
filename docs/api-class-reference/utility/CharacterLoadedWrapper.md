---
sidebar_position: 5
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

CharacterLoadedWrapper - special wrapper for Player which tracks Character's state. 
This differs from `Player.CharacterAdded` and `Player.CharacterAppearanceLoaded` which fire
before a character is parented to workspace and does not guarantee these other conditions.
We need this because there are some cases where a character can be removed without the humanoid dying,
such as if `:LoadCharacter()` is called before a character dies. Cleanup code often needs to run when a
character's **lifespan** is over, whether it be because the humanoid died or because the character is removed.
To avoid having to connect to both events in multiple places, this wrapper moves both events into one.

:::info
This is a preffered workflow, because the behavior of this wrapper is guaranteed to be consistent and safe.
:::

## Properties

---

### > `Loaded: Signal.Signal<Model>` <Tag color="#e3ce8b">Public</Tag>
Fires when player's character model is fully loaded.

---

### > `Died: Signal.Signal<Model>` <Tag color="#e3ce8b">Public</Tag>
Fires when player's character either *died* or character model was deleted from workspace.

---

### > `_player: Player` <Tag color="#4958df">Private</Tag>

---
### > `_destroyed: boolean` <Tag color="#4958df">Private</Tag>

---
### > `_connections: { RBXScriptConnection }` <Tag color="#4958df">Private</Tag>

---

## Constructor
---
### > `CharacterLoadedWrapper.new(player: Player)`
```lua title="ServerScriptService/PlayerManagment.server.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local CharacterLoadedWrapper = require(Modules.Utility.CharacterLoadedWrapper)

-- [Services] --
local Players = game:GetService("Players")

-- [Functions] --

-- Create new CharacterLoader which will observe characters state
local function onPlayerAdded(player: Player)
    local characterLoader = CharacterLoadedWrapper.new(player)

    characterLoader.Loaded:Connect(function(character)
        print(`[{script.Name}]: Spawned {character}.`)
    end)

    characterLoader.Died:Connect(function(character)
        print(`[{script.Name}]: {character} died.`)
    end)
end

-- [Main] --
for _, player in Players:GetPlayers() do
    onPlayerAdded(player)
end

Players.PlayerAdded:Connect(onPlayerAdded)
```

## Methods
---

### `CharacterLoadedWrapper:IsLoaded(optionalCharacter: Model?): boolean` <Tag color="#e3ce8b">Public</Tag>
Returns true if character passes these checks:
- Has PrimaryPart set
- Humanoid is Alive (not in `Enum.HumanoidStateType.Dead` and `Health` > 0)
- Descendant of workspace (indicates that character fully loaded)

---
### `CharacterLoadedWrapper:_listenForCharacterAdded(): ()` <Tag color="#4958df">Private</Tag>
Starts listening for player's character state.

---
### `CharacterLoadedWrapper:_waitForLoadedAsync(character: Model): ()` <Tag color="#4958df">Private</Tag>
Waits asynchronously for player's character to load.
This function assumes the character exists when it's called and has default behavior,
i.e. developer is not parenting the character somewhere manually.

:::warning
This method Yields!
:::

---
### `CharacterLoadedWrapper:_listenForDeath(character: Model): ()` <Tag color="#4958df">Private</Tag>
Debounce to prevent deferred events from letting .Died event fire more than once,
such as if the humanoid dies and the character is destroyed in the same compute cycle.
With deferred events, that would fire both events on the next cycle, even if the connection
is disconnected within the response to the event.

---
### `CharacterLoadedWrapper:Destroy(): ()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the CharacterLoadedWrapper, releasing it from memory.

---