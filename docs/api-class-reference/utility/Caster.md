---
sidebar_position: 3
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

Caster - utility class for raycasting which has debug mode built-in. Supports :Raycast(), :Blockcast() and :Spherecast()

![caster-debug1](https://cdn.discordapp.com/attachments/1192299550166241303/1368219759220359239/image.png?ex=682696b2&is=68254532&hm=f56c3653f99a184ca942478a340d0c60bac644f3260751bea730af472ab7b045&)
![caster-debug2](https://cdn.discordapp.com/attachments/1192299550166241303/1368219759505838120/image.png?ex=682696b2&is=68254532&hm=105a9ef05150ab5f760ea06bec04b9953391ed83b04c245468a9b02fe032766c&)
![caster-debug3](https://cdn.discordapp.com/attachments/1192299550166241303/1368219759753171076/image.png?ex=682696b3&is=68254533&hm=fade5555e2f7f5d5b43f1fb408ad89f08295697b30f53d1014b50eb793a08d92&)
![caster-debug4](https://cdn.discordapp.com/attachments/1192299550166241303/1368176936639266896/image.png?ex=68266ed1&is=68251d51&hm=583b4758f9f60dfc9f8af382a07a9f84db1bf1aa5a0d052476384c4da9b6278c&)

## Types

---

```lua
type Config = {
	DisplayLimit: number?,
	Lifetime: number?,
	Color: Color3?,
	WorldRoot: WorldRoot?,
	Persitent: boolean?,
	Visualize: boolean?,
}
```

## Properties

---

### > `DisplayLimit: number` <Tag color="#e3ce8b">Public</Tag>
Limits the amount of visible debug ray's at once. Oldest debug ray's will be deleted.

---

### > `Lifetime: number` <Tag color="#e3ce8b">Public</Tag>
Determines how long will debug ray live, before being deleted.

---

### > `Color: Color3` <Tag color="#e3ce8b">Public</Tag>
Determines debug ray color.

---

### > `WorldRoot: WorldRoot` <Tag color="#e3ce8b">Public</Tag>
Determines debug ray WorldRoot (usefull if you have WorldRoot that is not **Workspace**)

---

### > `Persitent: boolean` <Tag color="#e3ce8b">Public</Tag>
Determines whether debug ray's are persistent or not.

---

### > `Visualize: boolean` <Tag color="#e3ce8b">Public</Tag>
Determines whether debug ray's are visible or not.

---

### > `_persistentParts: { Line: Part?, Sphere: Part?, Block: Part? }` <Tag color="#4958df">Private</Tag>

---

### > `_trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#4958df">Private</Tag>

---

## Constructor

### > `Caster.new(config: Config?)`

## Methods

### > `Caster:_updatePersistent(casterType: string, part: Part)` <Tag color="#4958df">Private</Tag>

---

### > `Caster:_storeInfo(target: Part, result: RaycastResult): ()` <Tag color="#4958df">Private</Tag>

---

### > `Caster:Raycast(origin: Vector3, direction: Vector3, raycastParams: RaycastParams?): RaycastResult?` <Tag color="#e3ce8b">Public</Tag>
Casts a raycasts.

---

### > `Caster:Spherecast(origin: Vector3, radius: number, direction: Vector3, raycastParams: RaycastParams?): RaycastResult?` <Tag color="#e3ce8b">Public</Tag>
Casts a spherecast.

---

### > `Caster:Blockcast(cframe: CFrame, size: Vector3, direction: Vector3, raycastParams: RaycastParams?): RaycastResult?` <Tag color="#e3ce8b">Public</Tag>
Casts a blockcast.

---

### > `Caster:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Caster, releasing it from memory.

---
