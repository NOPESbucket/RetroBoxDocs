---
sidebar_position: 13
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

PlayerManager - module which manages currently connected users on the server. Includes a collection of utility functions.

## Properties
---

### > `Amount: number`
Current amount of players on server.

---
### > `List: {[string]: Player}`
Array of players on server.

---
### > `PlayerAdded: Signal.Signal<Player>`
Fires when player joins the server.

---
### > `PlayerRemoving: Signal.Signal<Player>`
Fires when player leaves the server.

---
### > `GearAdded: Signal.Signal<Player, Tool>`
Fires when gear is added to players backpack.

---

## Methods
---

### > `PlayerList.GetArray(): {Player}` <Tag color="#6e4999">Static</Tag>
Returns an array of players (ordering is not guarenteed).

---
### > `PlayerList.GetCharacters(): {Model}` <Tag color="#6e4999">Static</Tag>
Returns an array of characters (ordering is not guarenteed).

---
### > `PlayerList.GetRandomPlayer(): Player` <Tag color="#6e4999">Static</Tag>
Gets a random player on the server.

---