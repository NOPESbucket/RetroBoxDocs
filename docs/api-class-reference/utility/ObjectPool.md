---
sidebar_position: 10
---

ObjectPool - special class used to avoid unnecessarily instantiating Instances.

## Properties
---

### > `InstancePoolsByClass: { [string]: { Instance } }`
An array of instances that are allocated.

---
### > `PoolSizePerType: number`
Determines pool size per instance type.

---
### > `Name: string`
Name of the ObjectPool.

## Methods

---
### > `ObjectPool:GetInstance: (className: string): Instance`
Retrieves the instance from the object pool by it's name.

---
### > `ObjectPool:ReturnInstance: (instance: Instance)`
Returns the instance back to it's object pool for later use.

---