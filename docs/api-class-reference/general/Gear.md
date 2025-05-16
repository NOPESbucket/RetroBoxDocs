---
sidebar_position: 10
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

Gear - base [Class](../core/Class.md) for Tool objects that player can equip and interact with. Works both `Server/Client`.

## Properties
---

### > `Tool: Tool` <Tag color="#e3ce8b">Public</Tag>
Reference to a tool [Gear](./Gear.md) object is binded to.

---
### > `Owner: Player` <Tag color="#e3ce8b">Public</Tag>
Reference to a owner of the tool.

---
### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
Reference to a character of the owner.

---

### > `ClickLocation: Signal.Signal<CFrame>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever player clicks while tool is equipped.

---
### > `_trove: Trove.Trove` <Tag color="#4958df">Private</Tag>

---
### > `_animator: Animator.AnimatorObj` <Tag color="#4958df">Private</Tag>

---
### > `_mouse: Mouse.Mouse` <Tag color="#4958df">Private</Tag>

---

## Methods
---

### > `Gear:IsEquipped(): boolean` <Tag color="#e3ce8b">Public</Tag>
Returns boolean of whether tool is equipped or not.

---
### > `Gear:_setupAnimations()` <Tag color="#4958df">Private</Tag>
Setups the animations and behaviors for the tool.

---
### > `Gear:Destroy()`
Destroy's the Gear, releasing it from memory.
