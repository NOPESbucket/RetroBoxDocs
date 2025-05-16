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

SoundReplicator - no description.

## Properties
---

### > `AudioFolder: Folder?`

---
### > `AudioCache: { [string]: boolean }`

---

## Methods
---

### > `SoundReplicator.SetAudioFolder(folder: Folder)` <Tag color="#6e4999">Static</Tag> <Tag color="#2596be">Server</Tag>

---
### > `SoundReplicator.GetAudioFolder(): Folder?` <Tag color="#6e4999">Static</Tag> <Tag color="#2596be">Server</Tag>

---
### > `SoundReplicator.PlaySound2DAll(sound: Sound | string, volume: number?)` <Tag color="#6e4999">Static</Tag> <Tag color="#2596be">Server</Tag>

---
### > `SoundReplicator.PlaySound3D(player: Player, sound: Sound | string, target: BasePart | Vector3, volume: number?, rollOffMaxDistance: number?, rollOffMinDistance: number?, rollOffMode: Enum.RollOffMode?)` <Tag color="#6e4999">Static</Tag> <Tag color="#2596be">Server</Tag>

---
### > `SoundReplicator.PlaySound3DAll(sound: Sound | string, target: BasePart | Vector3, volume: number?, rollOffMaxDistance: number?, rollOffMinDistance: number?, rollOffMode: Enum.RollOffMode?)` <Tag color="#6e4999">Static</Tag> <Tag color="#2596be">Server</Tag>

---