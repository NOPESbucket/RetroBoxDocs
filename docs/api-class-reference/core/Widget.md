---
sidebar_position: 3
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

Widget - a Gui object which allows create & re-use UI components together.

:::warning
This has been deprecated.
:::

## Properties

---

### > `_scope: Fusion.Scope` <Tag color="#4958df">Private</Tag>

---

### > `_trove: ` [`Trove.Trove`](../utility/Trove.md) <Tag color="#4958df">Private</Tag>

---

## Methods
---

### > `Widget.GetValue(self: Types.Widget, name: string): unknown`
Returns the value of the Property.

---

### > `Widget.GetFusionValue(self: Types.Widget, name: string): Fusion.Value<unknown>`
Returns the `Fusion.Value<any>` object of the Property.

---

### > `Widget.SetValue(self: Types.Widget, name: string, value: unknown): ()`
Sets the value of the Property.

---

### > `Widget.HookFusionValue(self: Types.Widget, value: Fusion.Value<any>, propertyName: string): ()`
Hooks the fusion value to a specfic property allowing it effectively listening to changes and update accordingly.

---