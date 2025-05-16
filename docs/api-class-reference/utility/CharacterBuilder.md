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

Caster - utility class for creating a players character copy with the use of Roblox API's.

## Methods

### > `CharacterBuilder.GetCharacterCopyR6(player: Player)` <Tag color="#6e4999">Static</Tag>
Returns Character model as R6 rig.

:::warning
This method Yields!
:::

---

### > `CharacterBuilder.GetCharacterCopy(player: Player)` <Tag color="#6e4999">Static</Tag>
Returns Character model player currently has (not in-game, but on the website).

:::warning
This method Yields!
:::

---
