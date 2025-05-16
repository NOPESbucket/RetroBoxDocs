---
sidebar_position: 8
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


Hitbox - special class which was made for easy to use and best response hitboxes. Instead of relying purely on Spatial Query API 
(e.g. `WorldRoot:GetPartBoundsInBox`, `WorldRoot:GetPartBoundsInRadius`, `WorldRoot:GetPartsInPart`) which you mostly do on server for security reasons. This hitbox implementation lets you set network ownership and based on that network owner checks for the collision results.
:::note
All of the data sent by client and collision results will be verified by server, before firing any events prior.
:::

```lua title="ServerScriptService/HitboxTest.server.lua"
-- [Modules] --
local Hitbox = require(game.ReplicatedStorage.Hitbox)

-- [Services] --
local Players = game:GetService("Players")

-- [Instances] --
local aliveCharacters = workspace.AliveCharacters

-- [Functions] --

local function createHitbox(position: Vector3, owner: Player?)	
	local hitbox = Hitbox.new({
		HitboxType = "Magnitude",
		Shape = "Box",
		Debug = true,
		Size = Vector3.new(7, 7, 6.5),
		CFrame = CFrame.new(position),
		Owner = owner,
	})
	hitbox:WeldTo(owner.Character.PrimaryPart, CFrame.new(0, 0, -4.5))
	hitbox.Hit:Connect(function(basePart)
		print("Hit:", basePart)
	end)
	hitbox.Exit:Connect(function(basePart)
		print("Exit:", basePart)
	end)
	hitbox.HumanoidHit:Connect(function(humanoid)
		if (owner and humanoid.Parent.Name == owner.Name) or false then
			return
		end
		print("HumanoidHit:", humanoid.Parent, humanoid)
	end)
	hitbox.HumanoidExit:Connect(function(humanoid)
		if (owner and humanoid.Parent.Name == owner.Name) or false then
			return
		end
		print("HumanoidExit:", humanoid.Parent, humanoid)
	end)
	
	hitbox:Start()
end

local function onPlayerAdded(player: Player)
	local character = player.Character
	if character then
		character.Parent = aliveCharacters
	end

	player.CharacterAdded:Connect(function(character)
		character.Parent = aliveCharacters
		
		task.wait(5)

		createHitbox(Vector3.new(0, 2, 0), player)
	end)
end

-- [Main] --

Players.PlayerAdded:Connect(onPlayerAdded)
for _, player in Players:GetPlayers() do
	onPlayerAdded(player)
end
```

## Types
---

### HitboxConfiguration 
```lua
type HitboxConfiguration = {
	HitboxType: "Magnitude" | "Spatial",
	Shape: "Box" | "Sphere",
	Owner: Player?,
	Id: number,
}
``` 
#### > `HitboxType: "Magnitude" | "Spatial"`
Sets the type of the Hitbox. If set to `Magnitude`, hitbox will perform magnitude checks which will determine the collision result
:::info
`Magnitude` checks will be based on the AABB (Axis Aligned Bounding Box) instead of the typical sphere.
:::
`Spatial` hitboxes use Roblox's [Spatial Query API](https://devforum.roblox.com/t/introducing-overlapparams-new-spatial-query-api/1435720) which may yield to better results, but takes longer to compute due to Roblox engine accounting for every part in Octree.

#### > `Shape: "Box" | "Sphere"`
Sets the hitbox collision Shape. Can be only `Box` or `Sphere` hitbox.

#### > `Owner: Player?`
Determines who's the owner of the hitbox and who will perform collision checks
:::note
All of the data and collisions sent from client are verified before firing any events prior.
:::
When Player is set as the network owner, hitbox will **BE** replicated to it and client will continuously check for collisions. If client detects collision it will sent data to server to verify.\
When Server is set as the network owner, hitbox will **NOT** be replicated and all of collision operations will be performed on server-side completely. Don't use server owned hitboxes when doing any kind of interaction player is responsible, best for NPC's or any other stuff server is in charge of.

---

### HitboxParams 
```lua
type HitboxParams = {
	HitboxType: "Magnitude" | "Spatial",
	Shape: "Box" | "Sphere",
	Debug: boolean,
	Size: Vector3,
	CFrame: CFrame?,
	Owner: Player?,
}
```

#### > `HitboxType: "Magnitude" | "Spatial"`
Sets the type of the Hitbox. If set to `Magnitude`, hitbox will perform magnitude checks which will determine the collision result
:::info
`Magnitude` checks will be based on the AABB (Axis Aligned Bounding Box) instead of the typical sphere.
:::
`Spatial` hitboxes use Roblox's [Spatial Query API](https://devforum.roblox.com/t/introducing-overlapparams-new-spatial-query-api/1435720) which may yield to better results, but takes longer to compute due to Roblox engine accounting for every part in Octree.

#### > `Shape: "Box" | "Sphere"`
Sets the hitbox collision Shape. Can be only `Box` or `Sphere` hitbox.

#### > `Debug: boolean`
Determines whether collision debug is enabled. If hitbox has network owner that's Player, debug collision will be shown on network owners side too.

#### > `Size: Vector3`
Sets the size of the Hitbox.

#### > `CFrame: CFrame?`
Sets the CFrame of the Hitbox in world space.

#### > `Owner: Player?`
Determines who's the owner of the hitbox and who will perform collision checks
:::note
All of the data and collisions sent from client are verified before firing any events prior.
:::
When Player is set as the network owner, hitbox will **BE** replicated to it and client will continuously check for collisions. If client detects collision it will sent data to server to verify.\
When Server is set as the network owner, hitbox will **NOT** be replicated and all of collision operations will be performed on server-side completely. Don't use server owned hitboxes when doing any kind of interaction player is responsible, best for NPC's or any other stuff server is in charge of.

## Properties

---
### > `Size: Vector3` <Tag color="#e3ce8b">Public</Tag>
Determines the Size of the hitbox.

---
### > `CFrame: CFrame` <Tag color="#e3ce8b">Public</Tag>
Current position and orientation of the hitbox in world.

---
### > `Debug: boolean` <Tag color="#e3ce8b">Public</Tag>
Determines whether debug hitboxes are visible or not. Don't use it in production it may cause huge lag with large amount of hitboxes.

---
### > `Hit: Signal.Signal<BasePart>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever a [BasePart](https://create.roblox.com/docs/reference/engine/classes/BasePart) enters the hitbox.

---
### > `Exit: Signal.Signal<BasePart>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever a [BasePart](https://create.roblox.com/docs/reference/engine/classes/BasePart) exits the hitbox, if it was inside before.

---
### > `HumanoidHit: Signal.Signal<Humanoid>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever a [Humanoid](https://create.roblox.com/docs/reference/engine/classes/Humanoid) Character enters the hitbox.

---
### > `HumanoidExit: Signal.Signal<Humanoid>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever a [Humanoid](https://create.roblox.com/docs/reference/engine/classes/Humanoid) Character exits the hitbox, if it was inside before.

---

### > `_hitboxOctree: ` [`DOS`](./DynamicOctree.md) <Tag color="#4958df">Private</Tag>
Reference to the Octree which hitbox uses to track objects.

---
### > `_trackedInstances: { [Model]: BasePart }` <Tag color="#4958df">Private</Tag>
Reference to a HashMap of tracked Character's.

---
### > `_collidedInstances: { [Model]: { [BasePart]: boolean } }` <Tag color="#4958df">Private</Tag>
Reference to a HashMap of currently colliding [BaseParts](https://create.roblox.com/docs/reference/engine/classes/BasePart).

---
### > `_collidedHumanoids: { [Model]: boolean }` <Tag color="#4958df">Private</Tag>
Reference to a HashMap of currently colliding [Humanoids](https://create.roblox.com/docs/reference/engine/classes/Humanoid).

---
### > `_previousProperties: { [string]: any }` <Tag color="#4958df">Private</Tag>

---
### > `_history: { any }` <Tag color="#4958df">Private</Tag>
Reference to a previously recorded CFrames of the tracked objects. This is used to rewind to a certain point in time to verify a collision sent by client.
:::note
_history is used in `Magnitude` hitboxes only, `Spatial` hitboxes don't have support for it yet.
:::

---
### > `_hitboxPart: Part` <Tag color="#4958df">Private</Tag>
Reference to a Part which represents the hitbox in world. Primaraly used for debug purposes.

---
### > `_partWeld: BasePart?` <Tag color="#4958df">Private</Tag>

---
### > `_velocity: Vector3` <Tag color="#4958df">Private</Tag>


---
### > `_lastCFrame: CFrame` <Tag color="#4958df">Private</Tag>
Previous CFrame to the last processed CFrame.

---
### > `_weldOffset: CFrame` <Tag color="#4958df">Private</Tag>
---
### > `_trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#4958df">Private</Tag>
---
### > `_enabled: boolean` <Tag color="#4958df">Private</Tag>
Determines whether hitbox is active or not.

---
### > `_steppedConnection: RBXScriptConnection?` <Tag color="#4958df">Private</Tag>
Reference to a [RunService.Stepped](https://create.roblox.com/docs/reference/engine/classes/RunService#Stepped) [RBXScriptConnection](https://create.roblox.com/docs/reference/engine/datatypes/RBXScriptConnection).

---
### > `_config: HitboxConfiguration` <Tag color="#4958df">Private</Tag> <Tag color="#E66F59">🔒Read-Only</Tag>
A Read-Only reference of the passed `HitboxConfiguration` which is used to setup hitbox and later replicate the hitbox state to the client if network owner is set.

---

## Constructors
---

### > `Hitbox.new(hitboxParams: HitboxParams)`

## Methods
---

### `Hitbox:ClearTaggedChars()` <Tag color="#e3ce8b">Public</Tag>

---
### `Hitbox:Start()` <Tag color="#e3ce8b">Public</Tag>
Starts the hitbox collision checking.

---
### `Hitbox:WeldTo(weldTo: BasePart, offset: CFrame)` <Tag color="#e3ce8b">Public</Tag>
Weld the hitbox to the specified BasePart with Offset. Hitbox will keep the orientation and position relative to the specified BasePart.

---
### `Hitbox:Unweld()` <Tag color="#e3ce8b">Public</Tag>
Unwelds the hitbox from the part to which it was welded to. Orientation will be kept to the last CFrame.

---
### `Hitbox:ChangeWeldOffset(newOffset: CFrame)` <Tag color="#e3ce8b">Public</Tag>
Changes the hitbox's weld offset. Hitbox must be welded before this method is called.

---
### `Hitbox:Stop()` <Tag color="#e3ce8b">Public</Tag>
Stops the hitbox collision checking.

---
### `Hitbox:_getClosestPosition(character: Model, now: number): Vector3` <Tag color="#4958df">Private</Tag>
Returns the closets position of the character to a hitbox. This method used for `Magnitude` hitbox tests.

---
### `Hitbox:_getCFrame(): CFrame` <Tag color="#4958df">Private</Tag>
Returns the hitbox CFrame.

---
### `Hitbox:_getRewindCFrame(character: Model, part: BasePart, desiredTime: number): CFrame?` <Tag color="#4958df">Private</Tag>
Returns the rewind cframe of the character's body part to a specific time. May not always return CFrame due to data being expired and removed. This method used for `Magnitude` hitbox tests.

---
### `Hitbox:_trackCharacter(character: Model)` <Tag color="#4958df">Private</Tag>
Starts tracking character.

---
### `Hitbox:_replicateProperties()` <Tag color="#4958df">Private</Tag>
Replicates properties of the hitbox to a network owner.

---
### `Hitbox:_updateDebugHitbox()` <Tag color="#4958df">Private</Tag>
Updates the debug part orientation.

---
### `Hitbox:_runSpatialQueryCollision()` <Tag color="#4958df">Private</Tag>
Runs the SpatialQueryCollision test.

---
### `Hitbox:_runMagnitudeCollision()` <Tag color="#4958df">Private</Tag>
Runs the MagnitudeCollision test.

---
### `Hitbox:_updateHitboxOctree()` <Tag color="#4958df">Private</Tag>
Updates the hitbox's Octree keeping data up to date.

---
### `Hitbox:_updateVelocity(dt: number)` <Tag color="#4958df">Private</Tag>
Updates the hitbox's velocity to compenstate for lag when welded to a part whose owner is **NOT** server.

---
### `Hitbox:_runMagnitudeQuery(character: Model, desiredTime: number?)` <Tag color="#4958df">Private</Tag>
Performs a magnitude query, checking against every tracked instance.

---
### `Hitbox:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Hitbox, releasing it from memory. Replicated hitboxes will be automatically deleted.

---