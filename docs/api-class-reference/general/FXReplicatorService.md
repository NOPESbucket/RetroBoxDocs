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

FXReplicatorService - module for replicating effects across clients.

## Methods
---

### > `FXReplicatorService.Init()` <Tag color="#6e4999">Static</Tag>
Initializes FXReplicatorService.

---
### > `FXReplicatorService.Replicate(MainPlayer: Player, ...)` <Tag color="#6e4999">Static</Tag>
Replicates the passed in data (`Data: {ToolName: string, EffectName: string, ExtraData: any}`).

---