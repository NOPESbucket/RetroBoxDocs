---
sidebar_position: 17
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

Throwable - class that allows you to create throwable tool objects with ease.

## Properties
---

### > `Configuration: ThrowableConfiguration`
Reference to ThrowableConfiguration instance.

---
### > `Tool: Tool` <Tag color="#e3ce8b">Public</Tag>
Reference to a tool.

---
### > `Owner: Player` <Tag color="#e3ce8b">Public</Tag>
Reference to the owner of the tool.

---
### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
Reference to the owner's character.

---
### > `ManualActivation: boolean` <Tag color="#e3ce8b">Public</Tag>
Sets whether `.Activated` event will be triggered by default or not. If you want to trigger the event use `:Activate()`

---
### > `Threw: Signal.Signal<BasePart>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever throwable instance is thrown.

---
### > `Destroying: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever throwable is getting destroyed via `:Destroy()`

---
### > `_direction: Vector3` <Tag color="#4958df">Private</Tag>

---
### > `_visible: boolean` <Tag color="#4958df">Private</Tag>

---
### > `_trove: Trove.Trove` <Tag color="#4958df">Private</Tag>

---
### > `_boneBuilder: BoneBuilder.BoneBuilder` <Tag color="#4958df">Private</Tag>

---
### > `_animator: any` <Tag color="#4958df">Private</Tag>

---
### > `_throwableInstance: any` <Tag color="#4958df">Private</Tag>

---
### > `_objectPool: { any }` <Tag color="#4958df">Private</Tag>

---
### > `_cooldown: Timer.Timer` <Tag color="#4958df">Private</Tag>

---

## Constructor
---

### > `Throwable.new(tool: Tool, throwable: any, animations: { Animation })`

## Methods
---

### > `Throwable.Throw(self: Types.Throwable, direction: Vector3)` <Tag color="#e3ce8b">Public</Tag>
Forces character to throw the throwable instance.

---
### > `Throwable._throw(self: Types.Throwable, direction: Vector3)` <Tag color="#4958df">Private</Tag>
Actually throws the instance.

---
### > `Throwable._createHandleBone(self: Types.Throwable)` <Tag color="#4958df">Private</Tag>
Creates a handle bone for proper animations.

---
### > `Throwable._setupAnimations(self: Types.Throwable)` <Tag color="#4958df">Private</Tag>
Setups and binds the appropriate animation behavior to tool.

---
### > `Throwable._initializeObjectPool(self: Types.Throwable)` <Tag color="#4958df">Private</Tag>
Initializes the object pool for throwable instances.

---
### > `Throwable._acquire(self: Types.Throwable): any` <Tag color="#4958df">Private</Tag>
Acquires instance from the object pool.

---
### > `Throwable._return(self: Types.Throwable, instance: any)` <Tag color="#4958df">Private</Tag>
Returns instance from the object pool.

---
### > `Throwable.Destroy(self: Types.Throwable)` <Tag color="#e3ce8b">Public</Tag>
Destroy's the Throwable, releasing it from memory.

---