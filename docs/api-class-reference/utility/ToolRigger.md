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

ToolRigger - special wrapper which will rig the tool automatically on equip and requires minimum setup.

## Properties

---
### > `Tool: Tool` <Tag color="#e3ce8b">Public</Tag>
A reference to binded tool.

---
### > `Owner: Player` <Tag color="#e3ce8b">Public</Tag>
A reference to the owner of the ToolRigger.

---
### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
A reference to character model which will get rigged.

---
### > `Configuration: Configuration` <Tag color="#e3ce8b">Public</Tag>
Reference to the configuration of the ToolRigger.

---
### > `_trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#4958df">Private</Tag>

---
### > `_boneBuilder: BoneBuilder.BoneBuilder` <Tag color="#4958df">Private</Tag>
Reference to a [BoneBuilder](./BoneBuilder.md) object which handles the rigging.
<!-- https://nopesbucket.github.io/retro-box-docs-test/docs/api-class-reference/utility/BoneBuilder -->
---
## Constructor

### `ToolRigger.new(tool: Tool, animationConfiguration: Configuration)`
AnimationConfiguration instance must have this structure.\
![animtionConfiguration](/img/AnimationConfigurationExample.png)

## Methods
---

### > `ToolRigger:_bindEquip()` <Tag color="#4958df">Private</Tag>
Bind the equip behavior to the tool.

---
### > `ToolRigger:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the ToolRigger, releasing it from memory.

---