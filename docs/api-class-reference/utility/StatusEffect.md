---
sidebar_position: 13
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

StatusEffect - no description.

## Properties
---

### > `Humanoid: Humanoid` <Tag color="#e3ce8b">Public</Tag>

---
### > `Effects: {func: (humanoid: Humanoid) -> ()?}` <Tag color="#e3ce8b">Public</Tag>

---
### > `Destroying: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>

---
### > `_timer: timer` <Tag color="#4958df">Private</Tag>

---
### > `_lingerTimer: timer` <Tag color="#4958df">Private</Tag>

---
### > `_trove: ` [`Trove.Trove`](../utility/Trove.md)<Tag color="#4958df">Private</Tag>

---
## Constructor

### > `StatusEffect.new(target: Model | Humanoid, updateTime: number?, lingerTime: number?)`

---
## Methods

### > `StatusEffect:ResetLingerTimer()` <Tag color="#e3ce8b">Public</Tag>

---
### > `StatusEffect:ChangeUpdateTime(updateTime: number)` <Tag color="#e3ce8b">Public</Tag>

---
### > `StatusEffect:AddEffect(func: (humanoid: Humanoid) -> ())` <Tag color="#e3ce8b">Public</Tag>

---
### > `StatusEffect:Destroy( <Tag color="#e3ce8b">Public</Tag>
Destroy's the StatusEffect, releasing it from memory.

---