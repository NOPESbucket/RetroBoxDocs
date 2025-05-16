---
sidebar_position: 2
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

Animator - is an abstraction class which allows for much easier animation in **Roblox**. 
Instead of trying to find the animator inside the character and load the animations individually, Animator allows you to pass in the character, load animations in batch and play them by name.
This streamlines the process of adding animation in-game.

## Properties
---

### > `Character: Model` <Tag color="#e3ce8b">Public</Tag>
Reference to Character model that is animated.

---
### > `Animator: Animator` <Tag color="#e3ce8b">Public</Tag>
Reference to [Animator](https://create.roblox.com/docs/reference/engine/classes/Animator) of the Character.

---
### > `CurrentAnimation: AnimationTrack` <Tag color="#e3ce8b">Public</Tag>
Reference to a currently played animation track.

---
### > `AnimationRegistry: { [string]: AnimationTrack }` <Tag color="#e3ce8b">Public</Tag>
A registry which contains every loaded animation.

---
### > `AnimationIdRegistry: { [string]: string }` <Tag color="#e3ce8b">Public</Tag>
A registry which contains every ID of loaded animation.

---
### > `Started: Signal.Signal<string>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever animation started playing through [`:Play()`](Animator.md#-animatorplayanimationname-string-public) method of the [`AnimatorObj`](./Animator.md).

---
### > `Stopped: Signal.Signal<string>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever animation ended (but not interpolated to default position) it's playback or when [`:Stop()`](Animator.md#-animatorstopanimationname-string-public) method is called.

---
### > `Ended: Signal.Signal<string>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever animation completelly ended it's playback.

---
### > `MarkerReached: Signal.Signal<Player, string>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever marker is reached in the animation playback, allowing to bind specific behavior to the animation.

---
### > `SoundPlayed: Signal.Signal<Sound>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever sound was played in the animation playback, allowing to bind specific behavior to the animation.

---
### > `Destroying: Signal.Signal<nil>` <Tag color="#e3ce8b">Public</Tag>
Fires whenever [`AnimatorObj`](./Animator.md) is being destroyed via [`:Destroy()`](./Animator.md#-animatordestroy-public) method.

---
### > `_trove: Trove.Trove` <Tag color="#4958df">Private</Tag>

---

## Constructor

### > `Animator.new(character: Model, animations: { Animation })`

---

## Method
---

### > `Animator:GetCurrentAnimation(): AnimationTrack?` <Tag color="#e3ce8b">Public</Tag>
Returns currently played animation. May not return [AnimationTrack](https://create.roblox.com/docs/reference/engine/classes/AnimationTrack) if animation isn't playing.

---
### > `Animator:_loadAnimation(animation: Animation): boolean` <Tag color="#4958df">Private</Tag>
Loads the animation inside the [`AnimatorObj`](./Animator.md) allowing it to be played via [`:Play()`](Animator.md#-animatorplayanimationname-string-public).

---
### > `Animator:StopAll()` <Tag color="#e3ce8b">Public</Tag>
Stop's every animation that's currently playing in the [`AnimatorObj`](./Animator.md).

---
### > `Animator:Play(animationName: string)` <Tag color="#e3ce8b">Public</Tag>
Play's the animation.

---
### > `Animator:Stop(animationName: string)` <Tag color="#e3ce8b">Public</Tag>
Stop's the animation.

---
### > `Animator:ConnectMarkerReachedSignal(animationName: string, markerName: string, callback: () -> ()): RBXScriptConnection?` <Tag color="#e3ce8b">Public</Tag>
Connects a function callback to the animation with the specified marker. May not return [RBXScriptConnection](https://create.roblox.com/docs/reference/engine/datatypes/RBXScriptConnection) if invalid names was passed.

---
### > `Animator:GetAnimation(animationName: string): AnimationTrack?` <Tag color="#e3ce8b">Public</Tag>
Returns the [AnimationTrack](https://create.roblox.com/docs/reference/engine/classes/AnimationTrack). May not return [AnimationTrack](https://create.roblox.com/docs/reference/engine/classes/AnimationTrack) if invalid names was passed.

---
### > `Animator:GetAnimationAssetId(animationName: string): string?` <Tag color="#e3ce8b">Public</Tag>
Returns the animation AssetId. May not return AssetId if invalid names was passed.

---
### > `Animator:IsPlaying(animationName: string): boolean` <Tag color="#e3ce8b">Public</Tag>
Return boolean of whether animation is playing currently or not.

---
### > `Animator:AdjustSpeedAndPlay(animationName: string, speed: number)` <Tag color="#e3ce8b">Public</Tag>
Play's the animation with the specified speed.

---
### > `Animator:Destroy()` <Tag color="#e3ce8b">Public</Tag>
Destroy's the [`AnimatorObj`](./Animator.md), releasing it from memory.

---