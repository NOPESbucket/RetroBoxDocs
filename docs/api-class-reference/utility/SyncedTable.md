---
sidebar_position: 15
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

SyncedTable - is a data type which will sync data of the table between one or multiple clients and a server allowing a either **one-way** or **two-way** communication storage.

## Types
---
```lua
type SyncedTableEnum = {
    ONE_WAY_COMMUNICATION = 1,
    TWO_WAY_COMMUNICATION = 2
}
```

### > `SyncedTableEnum.ONE_WAY_COMMUNICATION`
Only server is authorized to sync table with client

### > `SyncedTableEnum.TWO_WAY_COMMUNICATION`
Both server and client are authorized to sync table

## Properties
---

### > `content: {T}` <Tag color="#e3ce8b">Public</Tag>
Table content that will be synced.

---
### > `mode: SyncedTableEnum` <Tag color="#e3ce8b">Public</Tag>
Determines in what mode the table will be able to sync.

---
### > `tableID: string` <Tag color="#e3ce8b">Public</Tag>
An ID that represent a table that will be synced with.

---
### > `TableSynced: Signal.Signal<{T}>` <Tag color="#e3ce8b">Public</Tag>
This event fires whenever table is synced.

---
### > `_syncTableConnection: string` <Tag color="#4958df">Private</Tag>
A string that represent the Remote connection.

---
### > `_player: Player` <Tag color="#4958df">Private</Tag>
A player to whom table will get synced with

---

## Constructor
---

### > `SyncedTable.new<T>(mode: SyncedTableEnum, tableID: string, player: Player?)`
:::note
You don't need to pass a player reference on client-side.
:::

## Methods
---

### > `SyncedTable:SetTable<T>(t: {T})` <Tag color="#e3ce8b">Public</Tag>
Sets the table.

---
### > `SyncedTable:GetTable<T>(): {T}` <Tag color="#e3ce8b">Public</Tag>
Returns the mutable table.

---
### > `SyncedTable:Sync<T>()` <Tag color="#e3ce8b">Public</Tag>
Sync the table with the client.

---
### > `SyncedTable:AwaitSync<T>()` <Tag color="#e3ce8b">Public</Tag>
Sync the table with the client.

:::warning
This method Yields!
:::

---
### > `SyncedTable:Destroy<T>()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the CharacterLoadedWrapper, releasing it from memory.
:::note
SyncedTables created on client are not deleted, so keep that in mind.
:::

---