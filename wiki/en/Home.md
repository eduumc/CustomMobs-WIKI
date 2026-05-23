# CustomMobs Plugin — English Wiki

> Version 2.0 | Paper/Spigot 1.18–1.21 | Java 17+

---

## Table of Contents

1. [Installation](#installation)
2. [File Structure](#file-structure)
3. [Commands](#commands)
4. [Permissions](#permissions)
5. [Creating a Custom Mob](#creating-a-custom-mob)
6. [AI Modes](#ai-modes)
7. [Phase System](#phase-system)
8. [Abilities](#abilities)
9. [Drop System](#drop-system)
10. [Spawn System](#spawn-system)
11. [Portal System](#portal-system)
12. [Dimension System](#dimension-system)
13. [Boss System](#boss-system)
14. [GUI Management](#gui-management)
15. [Multilanguage](#multilanguage)
16. [Version Notifier](#version-notifier)
17. [Color Codes Reference](#color-codes-reference)
18. [FAQ](#faq)

---

## Installation

1. Download the latest `.jar` from [Releases](../../../releases/latest)
2. Place it in your `plugins/` folder
3. Start the server — all config files are generated automatically
4. Edit files in `plugins/CustomMobPlugin/` as needed
5. Use `/cm reload` to apply changes without restarting

**Requirements:**
- Paper or Spigot 1.18 – 1.21.x
- Java 17+
- Paper 1.20+ required for custom dimensions
- WorldEdit or FAWE optional (for schematic portals/dimensions)

---

## File Structure

```
plugins/CustomMobPlugin/
├── config.yml                  ← Global settings only
├── mobs/
│   ├── forest_stalker.yml      ← One file per mob
│   ├── shadow_overlord.yml
│   └── your_mob.yml
├── portals/
│   └── shadow_realm_portal.yml
├── dimensions/
│   └── shadow_realm.yml
└── lang/
    ├── messages_en.yml
    └── messages_es.yml
```

**Each mob is its own YAML file** in the `mobs/` folder. The filename (without `.yml`) becomes the mob's ID.

---

## Commands

All commands use `/custommob` with aliases `/cmob` and `/cm`.

| Command | Description | Permission |
|---|---|---|
| `/cm list` | List all loaded mobs | `custommobs.use` |
| `/cm spawn <id> [amount]` | Spawn a mob at your location | `custommobs.spawn` |
| `/cm info <id>` | Show mob details | `custommobs.info` |
| `/cm kill <id\|all>` | Kill custom mobs | `custommobs.kill` |
| `/cm gui` | Open mob management GUI | `custommobs.gui` |
| `/cm dim <name>` | Teleport to a dimension | `custommobs.admin` |
| `/cm dims` | List all dimensions and portals | `custommobs.use` |
| `/cm givesummoner <dim> [player]` | Give a boss summoner item | `custommobs.admin` |
| `/cm givekey <portal> [player]` | Give a portal activation key | `custommobs.givekey` |
| `/cm spawnboss <dim>` | Force spawn dimension boss | `custommobs.admin` |
| `/cm skipcooldown <player> <dim>` | Skip entry cooldown | `custommobs.skipcooldown` |
| `/cm cooldown <dim>` | Check your cooldown | `custommobs.use` |
| `/cm reload` | Reload all configuration | `custommobs.admin` |

---

## Permissions

| Permission | Description | Default |
|---|---|---|
| `custommobs.use` | Basic access (list, dims, cooldown) | Everyone |
| `custommobs.info` | View mob details | Everyone |
| `custommobs.spawn` | Spawn mobs with commands | OP |
| `custommobs.kill` | Kill custom mobs | OP |
| `custommobs.gui` | Access the GUI | OP |
| `custommobs.givekey` | Give portal keys | OP |
| `custommobs.skipcooldown` | Skip dimension cooldown | OP |
| `custommobs.admin` | Full admin access | OP |
| `custommobs.*` | All permissions | OP |

---

## Creating a Custom Mob

### Via GUI (Recommended)

1. Run `/cm gui`
2. Click **+ Create Mob**
3. Type the mob ID (step 1)
4. Click the base entity button — browse eggs or type manually (step 2)
5. Type the display name (step 3)
6. The mob file is created automatically in `mobs/<id>.yml`
7. Edit all other settings from the GUI

### Via YAML File

Create a file at `plugins/CustomMobPlugin/mobs/your_mob_id.yml`:

```yaml
enabled: true
display-name: "&cFire Zombie"
base-entity: ZOMBIE
ai-mode: BASIC          # BASIC | ADVANCED | EPIC
is-boss: false

attributes:
  max-health: 60.0
  attack-damage: 8.0
  movement-speed: 0.30
  armor: 4.0
  armor-toughness: 1.0
  follow-range: 40.0
  knockback-resistance: 0.2
  scale: 1.0            # Requires 1.20.5+

equipment:
  helmet: LEATHER_HELMET
  chestplate: LEATHER_CHESTPLATE
  leggings: LEATHER_LEGGINGS
  boots: LEATHER_BOOTS
  mainhand: STONE_SWORD
  offhand: NONE
  drop-chance: 0.05

visual:
  glow: true
  glow-color: RED
  particles-on-spawn: FLAME
  fire-on-spawn: true

sounds:
  on-spawn: ENTITY_ZOMBIE_AMBIENT
  on-death: ENTITY_ZOMBIE_DEATH
  on-attack: ENTITY_ZOMBIE_ATTACK_IRON_DOOR
  on-phase-change: ENTITY_LIGHTNING_BOLT_THUNDER

spawn:
  mode: NATURAL         # NATURAL | TIMED | COMMAND_ONLY
  worlds:
    - world
  biomes:
    - FOREST
    - DARK_FOREST
  time: NIGHT           # DAY | NIGHT | ANY
  min-y: 0
  max-y: 128
  min-x: -5000
  max-x: 5000
  min-z: -5000
  max-z: 5000
  spawn-interval-ticks: 6000
  max-simultaneous: 10
  group-min: 1
  group-max: 3
  max-light-level: 7
  natural-despawn: true

drops:
  exp-min: 10
  exp-max: 30
  items:
    - material: ROTTEN_FLESH
      amount-min: 1
      amount-max: 3
      chance: 0.8
    - material: DIAMOND
      amount-min: 1
      amount-max: 1
      chance: 0.05
      custom-name: "&bFire Diamond"
      lore:
        - "&7Dropped by the Fire Zombie"
      enchantments:
        FIRE_PROTECTION: 2

ai:
  target: PLAYERS       # PLAYERS | ANIMALS | PLAYERS_AND_ANIMALS | ALL_MOBS | ALL
  flee-below-health: 0.0
  call-for-help: false
```

### Available Base Entities

Any hostile Minecraft entity works as a base. Common options:
`ZOMBIE`, `SKELETON`, `SPIDER`, `CREEPER`, `BLAZE`, `WITHER_SKELETON`, `DROWNED`, `HUSK`, `STRAY`, `PILLAGER`, `VINDICATOR`, `EVOKER`, `PHANTOM`, `GHAST`, `HOGLIN`, `PIGLIN_BRUTE`, `ZOGLIN`

---

## AI Modes

### BASIC
Default AI with these additions:
- Configurable target type
- Flee behavior when health is low
- Call-for-help (alerts nearby same-type mobs)

### ADVANCED
Everything in BASIC plus:
- Multi-phase system with HP thresholds
- Special abilities on cooldown per phase

### EPIC
Everything in ADVANCED plus:
- Per-phase movement speed modifiers
- Phase transition effects (lightning, messages)
- Minion summoning on phase change
- Full boss mechanics

### Target Options

| Value | Attacks |
|---|---|
| `PLAYERS` | Players only |
| `ANIMALS` | Passive animals |
| `PLAYERS_AND_ANIMALS` | Players and animals |
| `ALL_MOBS` | Everything except players |
| `ALL` | Absolutely everything |

---

## Phase System

Phases activate when the mob's HP drops below each threshold.

```
100% ──── Phase 1 ──── 65% ──── Phase 2 ──── 30% ──── Phase 3
          (normal)              (faster)               (desperate)
```

```yaml
ai:
  phases:
    - name: "Awakening"
      health-threshold: 1.0       # Active from 100% to next threshold
      ability-cooldown: 60        # Ticks between abilities
      movement-speed-modifier: 1.0
      abilities:
        - SHADOW_STRIKE
        - DARKNESS_AURA
      phase-message: "&5The boss awakens..."
      phase-lightning: false
      summon-on-phase: false

    - name: "Rage"
      health-threshold: 0.6       # Activates below 60% HP
      ability-cooldown: 35
      movement-speed-modifier: 1.3
      abilities:
        - SHADOW_STRIKE
        - VOID_BOLT
      phase-message: "&c&lRAGE MODE!"
      phase-lightning: true
      summon-on-phase: true
```

---

## Abilities

Abilities are defined in `config.yml` under `abilities:` and referenced by name in phases.

| Ability | Description |
|---|---|
| `FIREBALL_BURST` | Launches multiple fireballs at the target |
| `FIRE_AURA` | Burns all players within a radius |
| `SPEED_BOOST` | Gives the mob a speed potion effect |
| `EXPLOSION` | Creates an explosion at the mob's location |
| `SHADOW_STRIKE` | Powerful hit that blinds and withers the target |
| `DARKNESS_AURA` | Blinds and slows all nearby players |
| `VOID_BOLT` | Deals damage and levitates the target |
| `SUMMON_MINIONS` | Spawns minion mobs defined in `ai.minion-mob` |
| `TELEPORT` | Teleports behind the current target |
| `SHADOW_NOVA` | Shockwave that pushes and damages all nearby players |
| `HEAL` | Heals the mob for a fraction of its max HP |

---

## Drop System

```yaml
drops:
  exp-min: 10
  exp-max: 30
  items:
    - material: DIAMOND
      amount-min: 1
      amount-max: 3
      chance: 0.25          # 0.0 = never | 1.0 = always
      custom-name: "&bMagic Diamond"
      lore:
        - "&7A special gem"
      enchantments:
        SHARPNESS: 5
        UNBREAKING: 3
      # Special tags:
      portal-key: shadow_realm_portal    # Makes this item a portal key
      dimension-summoner: shadow_realm   # Makes this item a boss summoner
```

> ⚠️ **Important:** `chance` must be between `0.0` and `1.0`. Using `1` means 100%, not 1%.

### Adding Drops from the GUI

In the drops panel, hold any item in your main hand and click **+ Add Item from Hand**. The plugin preserves:
- Material
- Custom name
- Lore
- Enchantments
- Portal key / summoner NBT tags

---

## Spawn System

| Mode | Description |
|---|---|
| `NATURAL` | Spawns periodically based on biome, time, and light level |
| `TIMED` | Spawns on fixed intervals regardless of conditions |
| `COMMAND_ONLY` | Only spawns via `/cm spawn` command |

**Tick reference:**

| Ticks | Time |
|---|---|
| 200 | 10 seconds |
| 1200 | 1 minute |
| 6000 | 5 minutes |
| 12000 | 10 minutes |
| 72000 | 1 hour |

---

## Portal System

Portals are physical structures in the world that teleport players to custom dimensions.

### Building a Portal Manually

1. Build the frame using the block configured in `frame-material`
2. Interior must be exactly `frame-width × frame-height` blocks of air
3. The plugin detects the frame automatically when you place the last block
4. Right-click the frame with the portal key item to activate

**Frame structure (4×5 interior with BLACKSTONE):**
```
■ ■ ■ ■ ■ ■   ← top row (frame-width + 2)
■ · · · · ■
■ · · · · ■   ← frame-height = 5 rows
■ · · · · ■
■ · · · · ■
■ · · · · ■
■ ■ ■ ■ ■ ■   ← bottom row
```

### Portal Configuration

```yaml
# portals/my_portal.yml
enabled: true
dimension: my_dimension

frame-material: BLACKSTONE
portal-material: PURPLE_STAINED_GLASS_PANE
frame-width: 4
frame-height: 5

# ITEM | AUTO | FLINT_AND_STEEL
activation: ITEM
igniter-portal-key: my_portal   # Portal key ID required to activate
igniter-consume: true
frame-breakable: true            # Can survival players break the frame?

auto-generate: true
auto-generate-count: 2
auto-generate-worlds:
  - world
auto-generate-min-x: -3000
auto-generate-max-x: 3000
auto-generate-min-z: -3000
auto-generate-max-z: 3000
auto-regenerate-minutes: 60

return-portal: true
return-portal-material: CRYING_OBSIDIAN
return-portal-always-active: true

particle-idle: PORTAL
particle-enter: WITCH
sound-activate: BLOCK_END_PORTAL_FRAME_FILL
sound-enter: ENTITY_ENDERMAN_TELEPORT
```

### Getting a Portal Key

```
/cm givekey <portal_id> [player]
```

Or configure a mob to drop one:
```yaml
drops:
  items:
    - material: ENDER_EYE
      chance: 0.1
      custom-name: "&5Portal Key"
      portal-key: shadow_realm_portal
```

---

## Dimension System

Custom dimensions are separate Minecraft worlds with exclusive mobs.

> **Requires Paper 1.20+**

```yaml
# dimensions/my_dimension.yml
enabled: true
world-name: "my_dimension"
environment: NORMAL     # NORMAL | NETHER | THE_END
generator: ""           # Leave empty for default generation

exclusive-mobs:
  - my_boss

# Block vanilla mob spawns (only your custom mobs spawn here)
block-vanilla-spawns: true
kill-ender-dragon: true   # Only for THE_END environment

gamerules:
  doMobSpawning: false
  doWeatherCycle: false
  doDaylightCycle: false
```

---

## Boss System

```yaml
boss-spawn-mode: SUMMONER   # AUTO | SUMMONER
dimension-boss: shadow_overlord
boss-spawn-offset-x: 0
boss-spawn-offset-y: 0
boss-spawn-offset-z: 10

# Countdown timer
countdown-enabled: true
countdown-seconds: 600
countdown-warning-seconds: [300, 60, 30, 10]
countdown-action: KILL_ALL  # KILL_ALL | TELEPORT_OUT | EMPOWER_BOSS

# Entry cooldown
cooldown-enabled: true
cooldown-minutes: 30
cooldown-message: "&cWait &e{time} &cbefore entering again."

# Post-boss
clear-dimension-on-boss-death: true
teleport-out-on-boss-death: false
teleport-delay-seconds: 30
```

| Countdown Action | What happens |
|---|---|
| `KILL_ALL` | All players in the dimension die and are sent back |
| `TELEPORT_OUT` | Players are teleported out without dying |
| `EMPOWER_BOSS` | Boss heals to full HP and doubles speed |

### Summoner Item

If `boss-spawn-mode: SUMMONER`, players must use a summoner item inside the dimension to invoke the boss. Configure the drop in the mob's yml:

```yaml
drops:
  items:
    - material: NETHER_STAR
      chance: 0.05
      custom-name: "&5&lVoid Summoner"
      dimension-summoner: shadow_realm
```

Get one instantly with:
```
/cm givesummoner <dimension_id> [player]
```

---

## GUI Management

Open with `/cm gui`. Requires `custommobs.gui` permission.

### Main Panel
Shows all loaded mobs as player heads with stats. Click a head to manage that mob. Click **+ Create Mob** to create a new one.

### Mob Detail Panel
- **Spawn** — Spawns the mob at your location
- **Kill All** — Removes all living instances
- **Change Name** — Edit display name (chat input)
- **Edit Drops** — Opens drop editor
- **Change Target** — Select AI target type
- **Change Armor** — Assign equipment slots
- **Attributes** — Edit HP, damage, speed, armor
- **AI Mode** — Cycle between BASIC → ADVANCED → EPIC

### Drop Editor
- Left-click a drop to adjust its chance (chat input)
- Right-click a drop to remove it
- **+ Add Item from Hand** — Hold an item and click to add it as a drop, preserving all metadata

### Armor Editor
- Click **← Set from hand** for any slot while holding the item you want to assign
- Click **Clear** to remove an item from a slot

### Entity Selector (Create Flow)
When creating a mob, clicking the entity button opens a paged grid of all spawn eggs. Click an egg to select that entity type, or click **✎ Type manually** to write the entity name in chat.

---

## Multilanguage

Set the language in `config.yml`:
```yaml
settings:
  language: en   # en | es
```

Language files are at `plugins/CustomMobPlugin/lang/messages_en.yml` and can be freely edited. The plugin copies the default files on first startup.

---

## Version Notifier

The plugin automatically checks GitHub for new releases on startup. OP players and admins see a notification when they join if an update is available.

To disable:
```yaml
settings:
  check-updates: false
```

---

## Color Codes Reference

| Code | Color/Format |
|---|---|
| `&0` | Black |
| `&1` | Dark Blue |
| `&2` | Dark Green |
| `&3` | Dark Cyan |
| `&4` | Dark Red |
| `&5` | Dark Purple |
| `&6` | Gold |
| `&7` | Gray |
| `&8` | Dark Gray |
| `&9` | Blue |
| `&a` | Green |
| `&b` | Cyan |
| `&c` | Red |
| `&d` | Pink |
| `&e` | Yellow |
| `&f` | White |
| `&l` | **Bold** |
| `&o` | *Italic* |
| `&n` | Underline |
| `&m` | Strikethrough |
| `&k` | Obfuscated |
| `&r` | Reset |

---

## FAQ

**Why won't my portal activate?**
Check the frame dimensions match `frame-width` and `frame-height` exactly. The interior must be empty air. Enable `debug: true` in config and check console when clicking.

**Why won't my mob attack animals?**
Bukkit doesn't natively support mobs attacking animals. The plugin scans for targets every 2 seconds. Make sure the animal is within the mob's `follow-range`.

**Why did the portal interior only partially fill?**
This was a bug in older versions. Make sure you're using v2.0+. The interior now fills completely using `setType(mat, false)` to prevent glass pane connections.

**Can I have multiple dimensions?**
Yes. Add one `.yml` per dimension in the `dimensions/` folder and one per portal in `portals/`.

**How do I create a flat dimension?**
Leave `generator: ""` and set `gamerules.doMobSpawning: false`. True flat worlds require a world management plugin like Multiverse-Core.

**The mob I created from the GUI won't spawn.**
Make sure the base entity is a valid living entity (e.g. `ZOMBIE`, not `ITEM` or `ARROW`). Check console for a warning message from the spawn validator.

wiki by edumc_
