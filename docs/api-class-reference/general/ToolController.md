---
sidebar_position: 18
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

ToolController - an abstraction layer for tool instance which adds more input events.

## Methods
---

### > `ToolController.createServerTool(tool: Tool)` <Tag color="#6e4999">Static</Tag>
Return new ServerTool.
---
### > `ToolController.createClientTool(tool: Tool)` <Tag color="#6e4999">Static</Tag>
Return new ClientTool.
---