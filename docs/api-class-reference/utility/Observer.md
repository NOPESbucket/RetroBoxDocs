---
sidebar_position: 11
---

Observer - is a pattern centers around observing the lifetime of a given state.

The "state" in question can be anything. It could be a color value, a position, a table, or anything else. Typically, current state can be grabbed immediately (e.g. `part.Color`), and further changes can be detected via some sort of signal (e.g. `part:GetPropertyChangedSignal("Color")`).

The observer pattern should provide two crucial elements:

1. Detect the current and all future changes to some state.
2. For a given observation, detect when that state changes to something else, thus to provide a way to clean up.\
The general layout of an observer should look like such:

```lua
local stopObserving = observeSomething(...params, function(state)
    -- Do something with "state". This runs every time state changes, including the initial state.

    return function()
        -- Cleanup. Called once "state" changes to something else, or the `stopObserving` function is called.
    end
end)

-- At anytime, the `stopObserving` function can be called to stop the above observer and clean up
-- and currently-existing observations:
stopObserving()
```

Full documentation [here](https://sleitnick.github.io/RbxObservers/docs/observer-pattern)