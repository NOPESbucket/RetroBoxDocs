---
sidebar_position: 6
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

BehaviorBuilder - module for creating, setuping and attaching behavior tree's to Characters.

## Methods
---

### > `BehaviorBuilder.InitNPC(npc: Model, behaviorTree: Folder, blackboard: {[string]: any}, agentSettings: PathPlus.AgentParameters?): Model` <Tag color="#6e4999">Static</Tag>
Creates a new behavior tree for the NPC.
```lua title="ServerScriptService/BehaviorTreeNPCs.server.lua"
-- [Packages] --
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local ServerStorage = game:GetService("ServerStorage")

-- [Modules] --
local BehaviorBuilder = require(ReplicatedStorage.Modules.General.BehaviorBuilder)

-- [Instances] --
local bossTemplate = ServerStorage.SpawnInstances.NPCs.Bosses:FindFirstChild("Noob CommanderV2")
local behaviorTree = ServerStorage.Trees:FindFirstChild("Noob CommanderV2" .. "Tree")

-- [Variables] --
local blackboard = { -- Initial BlackBoard State
	IsDead = false,
	Target = nil,
	AttackInUse = false,
	PhaseTwo = false,
	CurrentPhase = 1
}

-- Initialize NPC with navigation parameters
local npc = BehaviorBuilder.InitNPC(
	bossTemplate, 
	behaviorTree, 
	blackboard, 
	{
		AgentRadius = 10,
		AgentHeight = 13,
		AgentCanJump = true,
		AgentCanClimb = false
	}
)
```