---
sidebar_position: 8
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

`Author: etithespir`

FastCastRedux - module used for creating projectiles with custom simulated physics.

Full documentation [here](https://etithespir.it/FastCastAPIDocs/).

:::note
This is a modified version of the FastCastRedux to support jump times in the simulation and different projectile casters.
:::

## Methods
---

### > `FastCast:Fire(origin: Vector3, direction: Vector3, velocity: Vector3 | number, castDataPacket: FastCastBehavior?, preSimulation: number?)` <Tag color="#6e4999">Static</Tag>
Fires a Caster.