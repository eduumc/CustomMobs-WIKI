

# ✅ Requirements

| Software          | Version     |
| ----------------- | ----------- |
| Java              | 17+         |
| Paper             | 1.18+       |
| Spigot            | 1.18+       |
| Custom Dimensions | Paper 1.20+ |

---

# 📂 File Structure

```text
plugins/
└── CustomMobPlugin/
    └── config.yml
```

---

# ⚡ Commands

| Command                         | Description           |
| ------------------------------- | --------------------- |
| `/custommob list`               | List all mobs         |
| `/custommob spawn <id>`         | Spawn mob             |
| `/custommob info <id>`          | Show mob info         |
| `/custommob reload`             | Reload config         |
| `/custommob dim <name>`         | Teleport to dimension |
| `/custommob dims`               | List dimensions       |
| `/custommob spawnboss <dim>`    | Force boss spawn      |
| `/custommob givesummoner <dim>` | Give summoner item    |

---

# 🔑 Permissions

```text
custommobs.use
custommobs.info
custommobs.spawn
custommobs.admin
custommobs.*
```

---

# 👹 Creating a Custom Mob

```yaml
mobs:
  shadow_warrior:
    enabled: true
    display-name: "&5Shadow Warrior"
    base-entity: WITHER_SKELETON
    ai-mode: EPIC
    is-boss: true
```

---

# 🧠 AI Modes

## BASIC

* Vanilla enhanced AI
* Reinforcements
* Flee system

## ADVANCED

* Boss phases
* Abilities
* Cooldowns

## EPIC

* Dynamic speed
* Minion summoning
* Lightning effects
* Aggressive behavior changes

---

# ❤️ Boss Phases

```yaml
phases:
  - name: "Phase 1"
    health-threshold: 1.0
    abilities:
      - SHADOW_STRIKE

  - name: "Phase 2"
    health-threshold: 0.6
    abilities:
      - VOID_BOLT
```

---

# 🔥 Abilities

## Fireball Burst

```yaml
FIREBALL_BURST:
  count: 5
  speed: 1.5
```

## Shadow Strike

```yaml
SHADOW_STRIKE:
  damage-multiplier: 2.5
```

## Void Bolt

```yaml
VOID_BOLT:
  damage: 30.0
```

## Teleport

```yaml
TELEPORT:
  max-distance: 20.0
```

---

# 💎 Drops

```yaml
drops:
  exp-min: 10
  exp-max: 30

  items:
    - material: DIAMOND
      chance: 0.25
```

---

# 🌍 Spawn System

```yaml
spawn:
  mode: NATURAL

  worlds:
    - world

  biomes:
    - FOREST
```

## Spawn Modes

| Mode           | Description      |
| -------------- | ---------------- |
| `NATURAL`      | Natural spawning |
| `TIMED`        | Timed spawning   |
| `COMMAND_ONLY` | Command only     |

---

# 🌀 Portal System

```yaml
portals:
  shadow_portal:
    enabled: true
    dimension: shadow_realm

    frame-material: OBSIDIAN
    activation: ITEM
```

## Portal Activation

| Type              | Description   |
| ----------------- | ------------- |
| `AUTO`            | Always active |
| `ITEM`            | Requires item |
| `FLINT_AND_STEEL` | Flint & steel |

---

# 🌌 Dimensions

```yaml
dimensions:
  shadow_realm:
    enabled: true
    world-name: "shadow_realm"
    environment: NORMAL
```

---

# 👑 Dimension Bosses

```yaml
boss-spawn-mode: SUMMONER

dimension-boss: shadow_overlord
```

---

# ⏳ Countdown System

```yaml
countdown-enabled: true
countdown-seconds: 600
countdown-action: KILL_ALL
```

## Countdown Actions

| Action         | Effect           |
| -------------- | ---------------- |
| `KILL_ALL`     | Kill all players |
| `TELEPORT_OUT` | Kick players out |
| `EMPOWER_BOSS` | Heal & buff boss |

---

# 🎨 Color Codes

```text
&a Green
&c Red
&5 Purple
&l Bold
&o Italic
&r Reset
```

---

# ❓ FAQ

## Portal won't activate

* Check frame size
* Check materials
* Check activation item
* Interior must be air

## Dimension won't generate

* Requires Paper 1.20+
* Requires Java 17+

---

# 🚀 Roadmap

* Mythic-style skills
* GUI editor
* Database support
* Mob leveling
* RPG progression
* PlaceholderAPI support

---

# 📜 License

MIT License

---

# ❤️ Credits

Made for edumc_
discord: eduardo_mc.
eonix studios link: ``` https://discord.gg/XbvxKhEN
```

