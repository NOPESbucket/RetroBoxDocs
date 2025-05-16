---
sidebar_position: 9
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

MouseModule - utility module used to replicate the behavior of Roblox's legacy [Mouse](https://create.roblox.com/docs/reference/engine/classes/Mouse) instance with the addition of usefull features.

## Properties
---

### > `collisionGroup: string`
Represents in which collision group mouse will test collision.

---
### > `filterDescendants: { any }`
An array of instance that will be filtered when performing collision test depending what `filerType` was set.

---
### > `filterType: Enum.RaycastFilterType`
Sets the filtering behavior for `filterDescendants` property.

---
### > `rayLenght: number`
Sets the lenght of how far mouse can test the collision.

---
### > `currentPosition: Vector2`
Current position of the mouse on a screen.

---
### > `previousPosition: Vector2`
Previous position of the mouse on a screen.

---
### > `ticks: number`
Last time when mouse was updated.

---

## Constructor
---

### > `Mouse.new()`

## Methods
---

### > `Mouse:GetViewSize(): Vector2`
Returns the viewport size in which mouse operates.

---
### > `Mouse:GetPosition(): Vector3`
Returns the current position of the mouse on the screen.

---
### > `Mouse:GetUnitRay(): Ray`
Returns the [Ray](https://create.roblox.com/docs/reference/engine/datatypes/Ray) of the mouse.

---
### > `Mouse:GetOrigin(): Vector3`
Returns the mouse origin in 3D world.

---
### > `Mouse:GetDelta(): Vector3`
Returns the mouse delta position.

---
### > `Mouse:ScreenPointToRay(): RaycastParameters`

---
### > `Mouse:CastRay()`
Casts a raycast in 3D world based on mouse position.

---
### > `Mouse:GetHit(): Vector3`
Returns the position what mouse is hitting in 3D world.

---
### > `Mouse:GetTarget()`
Returns what mouse is hitting in 3D world.

---
### > `Mouse:GetTargetFilter()`
Returns mouse's `filterDescendants`.

---
### > `Mouse:SetCollisionGroup(groupName: string)`
Sets the mouse's collision group to operate in.

---
### > `Mouse:SetTargetFilter(object: Instance | {Instance})`
Sets the mouse's `filterDescendants`. You can pass [Instance](https://create.roblox.com/docs/reference/engine/classes/Instance) or an array of [Instances](https://create.roblox.com/docs/reference/engine/classes/Instance).

---
### > `Mouse:GetRayLength()`
Returns the lenght of the mouse ray.

---
### > `Mouse:SetRayLength(length: number)`
Sets the lenght of the mouse ray.

---
### > `Mouse:GetFilterType(): Enum.RaycastFilterType`
Returns mouse's RaycastFilterType.

---
### > `Mouse:SetFilterType(filterType: Enum.RaycastFilterType)`
Sets mouse's RaycastFilterType.

---
### > `Mouse:EnableIcon()`
Enables mouse icon.

---
### > `Mouse:DisableIcon()`
Disables mouse icon.

---
### > `Mouse:Destroy()`
Destroy's the Mouse, releasing it from memory.

---