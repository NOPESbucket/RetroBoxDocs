---
sidebar_position: 4
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

AttackingAiSpawner (AAS) - no description.

## Properties
---

### > `Model: Model` <Tag color="#e3ce8b">Public</Tag>

---
### > `Trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#e3ce8b">Public</Tag>

---
### > `PathPlus: PathPlus` <Tag color="#e3ce8b">Public</Tag>

---
### > `Animator: ` [`Animator`](./Animator.md) <Tag color="#e3ce8b">Public</Tag>

---
### > `Module: unknown` <Tag color="#e3ce8b">Public</Tag>

---
### > `Target: Instance?` <Tag color="#e3ce8b">Public</Tag>

---
### > `targetsPreviousPos: Vector3` <Tag color="#e3ce8b">Public</Tag>

---
### > `_attackConnection: RBXScriptConnection` <Tag color="#4958df">Private</Tag>

---

## Constructor
---

### > `AAS.NewNpc(Model: Model, defaultSettings: PathPlus.AgentParameters, WhitelistPlayers : {any}?)`

---

## Methods
---

### > `AAS:Attack()` <Tag color="#e3ce8b">Public</Tag>

---
### > `AAS:StopAttack()` <Tag color="#e3ce8b">Public</Tag>

---
### > `AAS:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the AAS, releasing it from memory.

---