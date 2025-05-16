---
sidebar_position: 14
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

Ragdollify - module used for creating ragdolls for Characters.

## Properties

### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
Reference to character who will be ragdolled.

---
### > `Humanoid: Humanoid` <Tag color="#e3ce8b">Public</Tag>
Reference to humanoid of the character.

---
### > `Player: Player?` <Tag color="#e3ce8b">Public</Tag>
Reference to a player. May be nil of ragdoll was created on the NPC.

---
### > `Unragdolled: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires when [`:Unragdoll()`](./Ragdollify.md#-ragdollifyunragdoll-unragdollontouch-boolean-timeout-number) is called.

---
### > `Ragdolled: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires when [`:Ragdoll()`](./Ragdollify.md#-ragdollifyragdoll) is called.

---
### > `Touched: Signal.Signal<BasePart>` <Tag color="#e3ce8b">Public</Tag>
Fires when ragdoll's body part touches new part.

---
### > `TouchEnded: Signal.Signal<BasePart>` <Tag color="#e3ce8b">Public</Tag>
Fires when ragdoll's body part stop's touching touched part.

---
### > `_trove: Trove.Trove` <Tag color="#4958df">Private</Tag>

---
### > `_unragdollTimer: Timer.Timer` <Tag color="#4958df">Private</Tag>

---
### > `_torso: BasePart` <Tag color="#4958df">Private</Tag>

---
### > `_isRagdoll: BoolValue` <Tag color="#4958df">Private</Tag>

---

## Constructor
---

### > `Ragdollify.new(character: Model)`

## Methods
---

### > `Ragdollify:Ragdoll()` <Tag color="#e3ce8b">Public</Tag>
Forces character enter ragdoll.

---
### > `Ragdollify:Unragdoll(unragdollOnTouch: boolean?, timeout: number?)` <Tag color="#e3ce8b">Public</Tag>
Forces character exit ragdoll.

---
### > `Ragdollify:IsRagdolled(): boolean` <Tag color="#e3ce8b">Public</Tag>
Returns boolean of whether character in ragdoll state.

---
### > `Ragdollify:_attachListener()` <Tag color="#4958df">Private</Tag>
Attaches collision listeners to the characters body part for tracking collisions of the character.

---
### > `Ragdollify:_replaceJoints()` <Tag color="#4958df">Private</Tag>
Replaces every single bone ([Motor6D](https://create.roblox.com/docs/reference/engine/classes/Motor6D)) inside Character.

---
### > `Ragdollify:_resetJoints()` <Tag color="#4958df">Private</Tag>
Destroys all Ragdoll made instances and re-enables the [Motor6D's](https://create.roblox.com/docs/reference/engine/classes/Motor6D).

---
### > `Ragdollify:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Ragdoll, releasing it from memory.

---