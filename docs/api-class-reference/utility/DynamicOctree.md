---
sidebar_position: 7
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

`Module by: Plasmanode`\
**Official DevForum [post](https://devforum.roblox.com/t/dynamic-octree-system/2177042)**

Dynamic Octree System (DOS) - expansion of [Quenty’s Octree module](https://quenty.github.io/NevermoreEngine/api/Octree/) and makes it easy to track dynamic, moving objects. According to Quenty, Octrees work best for static objects (objects that are staying still), however they can still be used with moving objects.
This module is actually pretty simple! It lets you register objects to the Octree, so that when you update them it automatically removes the node at it’s old position.

## What are Octrees?
In essence, an Octree is sort of like a recursive chunk system.

An octree is a tree data structure in which each internal node has exactly eight children. Octrees are most often used to partition a three-dimensional space by recursively subdividing it into eight octants.

![Octree visualization](https://devforum-uploads.s3.dualstack.us-east-2.amazonaws.com/uploads/optimized/5X/e/c/4/3/ec4384970592733fa1afd8d3b5c726fd23d74e46_2_690x419.png)\
Basically, it’s useful because if you have a huge area, instead of filling it with a ton of small, precise chunks and sacrificing performance, or a few big chunks and sacrificing fidelity, you can create an Octree and it will automatically subdivide! Better yet, if nothing exists in a particular area… there won’t be any grid sections there! Saves memory!

## What this looks like in Roblox
Here’s a visualization I threw together. I am working on updating the Draw module included (made by Quenty), so we can visualize Dynamic Octrees in real time, and in a way that looks prettier and easier to see.
![Roblox octree example 1](https://devforum-uploads.s3.dualstack.us-east-2.amazonaws.com/uploads/original/5X/9/9/9/b/999b318e1b4d2487b28db775a266d57976839f48.jpeg)
![Roblox octree example 2](https://devforum-uploads.s3.dualstack.us-east-2.amazonaws.com/uploads/original/5X/1/4/0/4/1404d9c1744afb19cef207d215bc992150c4d54e.jpeg)

## Why use Octrees?
**Octrees are a very fast way to handle searching for nearby objects.** For example, if you need to compute collisions, instead of first checking the distance between every object and the player, you first see what objects are within a certain radius using `Octree:RadiusSearch(Pos, Dist)`, to get nearby objects. It’s pretty sweet!

```lua title="ServerScriptService/OctreeExample.server.lua"
local DOS = require(pathToDOSModule);

local Grid = DOS.New("Players", 4, 100);

game.Players.PlayerAdded:Connect(function (Player)
	local tracker;

	Player.CharacterAdded:Connect(function (Character)
		tracker = Grid:Track(Character.HumanoidRootPart, 0.1); -- Remember that using Grid:Track is not ideal for a large amount of objects. Better in this case to make a big loop to update for all players, or update only when movement events are fired.
	end);

	Player.CharacterRemoving:Connect(function (Character)
		if (tracker) then
			tracker:Destroy();
		end
	end);
end);


while true do
	task.wait(1);
	
	local nearby = Grid:RadiusSearch(Vector3.zero, 50);
	print("Nearby entities: ", nearby)
end
```

## Types
---
### > [OctreeNode](https://quenty.github.io/NevermoreEngine/api/OctreeNode)

## Properties
---
### > `Name: string` <Tag color="#e3ce8b">Public</Tag>
Name of the Octree Grid.

---
### > `Tree: DOS.Octree` <Tag color="#e3ce8b">Public</Tag>

---
### > `Update: boolean` <Tag color="#e3ce8b">Public</Tag>
Enables/disables tracked entry updates.

---
### > `Entires: {unknown}` <Tag color="#4958df">Private</Tag>

---
### > `Tracked: {unknown}` <Tag color="#4958df">Private</Tag>

## Constructor
---
### > `DOS.New(name: string, depth: number | 4, size: number | 512)`

## Methods
---

### `Grid:Add(instance: any, position: Vector3)` <Tag color="#e3ce8b">Public</Tag>
Adds item entry to the octree with specified position.

---
### `Grid:AddStatic(instance: any, position: Vector3)` <Tag color="#e3ce8b">Public</Tag>
Adds static item entry to the octree with specified position. Static entries will not be destroyed or moved within the lifespan of the DOS grid.

---
### `Grid:UpdateFor(instance: any, position: Vector3)` <Tag color="#e3ce8b">Public</Tag>
Updates item entry position for specified instance.

---
### `Grid:Track(instance: any, updateFrequency: number | 0.1)` <Tag color="#e3ce8b">Public</Tag>
Starts updating item entry with specified update frequency (default is 0.1).

:::warning
This is mainly for convenience, and should not be relied on or used for a large number of entries. It’s useful because you can give it an instance,
including a model (so long as it has a primary part) and a set interval at how often it should update. For a large number of dynamic entries,
it is best to implement your own update solution.
:::

---
### `Grid:RadiusSearch(position: Vector3, radius: number) -> ({T}, {number})` <Tag color="#e3ce8b">Public</Tag>
Performs radial search at specified position. Returns a tuble with array of item entries and array of distances of these item entries, if they are in radius.

---
### `Grid:GetAllNodes(): {OctreeNode<T>}` <Tag color="#e3ce8b">Public</Tag>
Returns array of all nodes in Octree Grid.

---
### `Grid:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Octree Grid, releasing it from memory.

---