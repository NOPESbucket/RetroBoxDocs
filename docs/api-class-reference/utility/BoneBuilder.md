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

BoneBuilder - utility module which allows for easy rigging at runtime.

## Types

---

```lua
type InstancePath = {
	Path: string,
	Root: Instance?,
}
```

```lua
type BoneParams = {
	Name: string,
	Part0: Instance | InstancePath,
	Part1: Instance | InstancePath,
	C0: CFrame,
	C1: CFrame,
	Parent: Instance,
}
```

## Properties

---

### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
Reference to a binded Character model.

---

### > `_trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#4958df">Private</Tag>

---

### > `_managedBones: { [string]: Motor6D }` <Tag color="#4958df">Private</Tag>

---

## Constructor

---

### > `BoneBuilder.new(character: Character)`

## Methods

---

### > `BoneBuilder:GetCharacter(): Model` <Tag color="#e3ce8b">Public</Tag>
Returns a reference to a binded Character model.

---

### > `BoneBuilder:CreateBone(params: BoneParams): Motor6D` <Tag color="#e3ce8b">Public</Tag>
Creates a bone with specified params.

```lua title="StarterPlayer/StarterCharacterScripts/Boner.client.lua"
-- [Packages] --
local Modules = game.ReplicatedStorage.Modules

-- [Modules] --
local BoneBuilder = require(Modules.Utility.BoneBuilder)

-- [Instances] --
local character = script.Parent

-- [Objects] --
local boneBuilder = BoneBuilder.new(character)

boneBuilder:CreateBone({
    Name = "Handle",
	Part0 = { Path = "Torso" }, -- Torso
	Part1 = { Path = "Left Arm" }, -- Handle
	C0 = CFrame.new(),
	C1 = CFrame.new(),
	Parent = { Path = "Torso" },
})
```

---

### > `BoneBuilder:GetBone(name: string): Motor6D?` <Tag color="#e3ce8b">Public</Tag>
Returns the Motor6D instance by name that was refered in BoneParams Name field.

---

### > `BoneBuilder:RemoveBone(name: string)` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Motor6D from the character.

---

### > `BoneBuilder:Destroy(): ()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the BoneBuilder, releasing it from memory.

---