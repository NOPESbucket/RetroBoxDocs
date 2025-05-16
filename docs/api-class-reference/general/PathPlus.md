---
sidebar_position: 11
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

PathPlus - abstraction module for [PathfindingService](https://create.roblox.com/docs/reference/engine/classes/PathfindingService) allowing for fast implementation to the pathfinding NPC's.\
Includes usefull features such as:
- Pathfinding Debug mode
- Unstuck mechanism
- Non-reliant to Humanoid events

## Types
---

```lua
type AgentParameters = {
	AgentRadius: number?,
	AgentHeight: number?,
	AgentCanJump: boolean?,
	AgentCanClimb: boolean?,
	WaypointSpacing: number?,
	Costs: { [string]: number }?,
}
```
For more info what each parameter does, go to Roblox documentation [here](https://create.roblox.com/docs/reference/engine/classes/PathfindingService#CreatePath).

## Properties

### > `Visualize: boolean` <Tag color="#e3ce8b">Public</Tag>

---
### > `OutputErrors: boolean` <Tag color="#e3ce8b">Public</Tag>

---
### > `StuckThreshold: number` <Tag color="#e3ce8b">Public</Tag>

---
### > `StuckTimeout: number` <Tag color="#e3ce8b">Public</Tag>

---
### > `DistanceThreshold: number` <Tag color="#e3ce8b">Public</Tag>

---

### > `WaypointReached: Signal.Signal<PathWaypoint>` <Tag color="#e3ce8b">Public</Tag>
Fires when reached waypoint.

---
### > `DestinationReached: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires when destination reached.

---
### > `Blocked: Signal.Signal<Instance?>` <Tag color="#e3ce8b">Public</Tag>
Fires when path was blocked.

---
### > `Stucked: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires when agent gets stuck.

---
### > `_moveToFinished: Signal.Signal<>` <Tag color="#4958df">Private</Tag>
Fires when humanoid finished moving to a specific point.

---
### > `_computationSuccess: boolean` <Tag color="#4958df">Private</Tag>

---
### > `_moving: boolean` <Tag color="#4958df">Private</Tag>

---
### > `_nextWaypointIndex: number` <Tag color="#4958df">Private</Tag>

---
### > `_lastPosition: Vector3` <Tag color="#4958df">Private</Tag>

---
### > `_lastDestination: Vector3` <Tag color="#4958df">Private</Tag>

---
### > `_waypoints: { PathWaypoint }` <Tag color="#4958df">Private</Tag>

---
### > `_connections: { [string]: RBXScriptConnection }` <Tag color="#4958df">Private</Tag>

---
### > `_visualWaypoints: { Part }` <Tag color="#4958df">Private</Tag>

---

### > `_humanoid: Humanoid` <Tag color="#4958df">Private</Tag>

---
### > `_humanoidRootPart: Part` <Tag color="#4958df">Private</Tag>

---
### > `_character: Model` <Tag color="#4958df">Private</Tag>

---
### > `_stuckTimer: any` <Tag color="#4958df">Private</Tag>

---
### > `_path: Path` <Tag color="#4958df">Private</Tag>

---
### > `_trove: Trove.Trove` <Tag color="#4958df">Private</Tag>

---

## Constructor
---

### > `PathPlus.new(character: Model, agentParameters: AgentParameters?)`

## Methods
---

### > `PathPlus.IsMoving(self: Pathfinder): boolean` <Tag color="#e3ce8b">Public</Tag>
Returns boolean of whether agent is moving or not.

---
### > `PathPlus.Compute(self: Pathfinder, target: BasePart | Vector3)` <Tag color="#e3ce8b">Public</Tag>
Computes path asynchronously to the target.

---
### > `PathPlus._update(self: Pathfinder)` <Tag color="#4958df">Private</Tag>
Update function to check for stuck behavior.

---
### > `PathPlus.MoveToNextWaypoint(self: Pathfinder)` <Tag color="#e3ce8b">Public</Tag>
Moves the agent to the next waypoint of the path.

---
### > `PathPlus.Stop(self: Pathfinder, stopMovement: boolean?)` <Tag color="#e3ce8b">Public</Tag>
Stop the agent from advancing the path forward.

---
### > `PathPlus.Destroy(self: Pathfinder)` <Tag color="#e3ce8b">Public</Tag>
Destroy's the PathPlus, releasing it from memory.

---