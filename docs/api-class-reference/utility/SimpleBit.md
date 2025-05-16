---
sidebar_position: 11
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

SimpleBit - is a super simple utility module that allows you easily edit 32-bit numbers with ease.

## Methods
---

### > `SimpleBit.setBit(num: number, pos: number)` <Tag color="#6e4999">Static</Tag>
Sets the bit to 1 at a specific position.
```lua
local SimpleBit = require(path.to.SimpleBit)

local num = 0 -- binary: 0000
local result = SimpleBit.setBit(num, 2) -- sets bit 2
print(result) -- Output: 2 (binary: 0010)
```

---
### > `SimpleBit.clearBit(num: number, pos: number)` <Tag color="#6e4999">Static</Tag>
Sets the bit to 0 at a specific position.
```lua
local num = 7 -- binary: 0111
local result = SimpleBit.clearBit(num, 2) -- clears bit 2
print(result) -- Output: 5 (binary: 0101)
```

---
### > `SimpleBit.flipBit(num: number, pos: number)` <Tag color="#6e4999">Static</Tag>
Flips the bit at a specific position.
```lua
local num = 4 -- binary: 0100
local result = SimpleBit.flipBit(num, 3) -- flips bit 3 (set to 0)
print(result) -- Output: 0 (binary: 0000)

local result2 = SimpleBit.flipBit(num, 2) -- flips bit 2 (set to 1)
print(result2) -- Output: 6 (binary: 0110)
```

---
### > `SimpleBit.checkBit(num: number, pos: number): boolean` <Tag color="#6e4999">Static</Tag>
Checks whether the bit is 1 or 0. Returns true if bit is set to 1.

```lua
local num = 5 -- binary: 0101
print(SimpleBit.checkBit(num, 1)) -- true (bit 1 is 1)
print(SimpleBit.checkBit(num, 2)) -- false (bit 2 is 0)
print(SimpleBit.checkBit(num, 3)) -- true (bit 3 is 1)
```

---