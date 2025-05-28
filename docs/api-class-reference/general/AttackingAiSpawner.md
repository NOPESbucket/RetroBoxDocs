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

AttackingAiSpawner (AAS) - The AAS(Attacking AI Spawner) module provides a framework for creating and managing NPCs with advanced pathfinding, targeting, and attack behaviours.

## Properties
---

### > `Model: Model` <Tag color="#e3ce8b">Public</Tag>
The Roblox Model to use for the NPC(must contain a Humanoid)
---
### > `Trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#e3ce8b">Public</Tag>

---
### > `PathPlus: PathPlus` <Tag color="#e3ce8b">Public</Tag>
Pathfinding controller
---
### > `Animator: ` [`Animator`](./Animator.md) <Tag color="#e3ce8b">Public</Tag>
Animation controller
---
### > `Module: unknown` <Tag color="#e3ce8b">Public</Tag>
NPC-specific behavior module
---
### > `Target: Instance?` <Tag color="#e3ce8b">Public</Tag>
Current target player
---
### > `targetsPreviousPos: Vector3` <Tag color="#e3ce8b">Public</Tag>
Previous position of a target player
---
### > `_attackConnection: RBXScriptConnection` <Tag color="#4958df">Private</Tag>
reference used to manage the NPC's attack behavior
---

## Constructor
---

### > `AAS.NewNpc(Model: Model, defaultSettings: PathPlus.AgentParameters, WhitelistPlayers : {any}?)`
Creates a new NPC instance with the specified configuration
---

## Methods
---

### > `AAS:Attack()` <Tag color="#e3ce8b">Public</Tag>
Starts the NPC's attack behavior: 
---
### > `AAS:StopAttack()` <Tag color="#e3ce8b">Public</Tag>
Stops all attack-related behaviors
---
### > `AAS:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the AAS, releasing it from memory.

---
