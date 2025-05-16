---
sidebar_position: 16
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

StunPlayer - module that lets you stun player character.

## Methods
---

### > `StunPlayer.Stun(Duration: number)` <Tag color="#6e4999">Static</Tag> <Tag color="#70E860">Client</Tag>
Stuns player character for specific duration (gently breaks your knees and heals them back).

---
### > `StunPlayer.PermanentStun()` <Tag color="#6e4999">Static</Tag> <Tag color="#70E860">Client</Tag>
Stuns player character permanently (makes you basically a disabled person in a wheelchair).

---
### > `StunPlayer.Unstun()` <Tag color="#6e4999">Static</Tag> <Tag color="#70E860">Client</Tag>
Unstuns player character by giving character legs back.

---