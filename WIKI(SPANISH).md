
````md
# ✅ Requisitos

| Software             | Versión      |
| -------------------- | ------------ |
| Java                 | 17+          |
| Paper                | 1.18+        |
| Spigot               | 1.18+        |
| Dimensiones Custom   | Paper 1.20+  |

---

# 📂 Estructura de Archivos

```text
plugins/
└── CustomMobPlugin/
    └── config.yml
````

---

# ⚡ Comandos

| Comando                         | Descripción                    |
| ------------------------------- | ------------------------------ |
| `/custommob list`               | Lista todos los mobs           |
| `/custommob spawn <id>`         | Spawnea un mob                 |
| `/custommob info <id>`          | Muestra información del mob    |
| `/custommob reload`             | Recarga la configuración       |
| `/custommob dim <nombre>`       | Teletransporta a una dimensión |
| `/custommob dims`               | Lista dimensiones              |
| `/custommob spawnboss <dim>`    | Fuerza el spawn del boss       |
| `/custommob givesummoner <dim>` | Da el item invocador           |

---

# 🔑 Permisos

```text
custommobs.use
custommobs.info
custommobs.spawn
custommobs.admin
custommobs.*
```

---

# 👹 Crear un Mob Custom

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

# 🧠 Modos de IA

## BASIC

* IA vanilla mejorada
* Refuerzos
* Sistema de huida

## ADVANCED

* Fases de boss
* Habilidades
* Cooldowns

## EPIC

* Velocidad dinámica
* Invocación de minions
* Efectos de rayos
* Cambios agresivos de comportamiento

---

# ❤️ Fases del Boss

```yaml
phases:
  - name: "Fase 1"
    health-threshold: 1.0
    abilities:
      - SHADOW_STRIKE

  - name: "Fase 2"
    health-threshold: 0.6
    abilities:
      - VOID_BOLT
```

---

# 🔥 Habilidades

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

# 🌍 Sistema de Spawn

```yaml
spawn:
  mode: NATURAL

  worlds:
    - world

  biomes:
    - FOREST
```

## Modos de Spawn

| Modo           | Descripción           |
| -------------- | --------------------- |
| `NATURAL`      | Spawn natural         |
| `TIMED`        | Spawn por tiempo      |
| `COMMAND_ONLY` | Solo mediante comando |

---

# 🌀 Sistema de Portales

```yaml
portals:
  shadow_portal:
    enabled: true
    dimension: shadow_realm

    frame-material: OBSIDIAN
    activation: ITEM
```

## Activación de Portales

| Tipo              | Descripción        |
| ----------------- | ------------------ |
| `AUTO`            | Siempre activo     |
| `ITEM`            | Requiere item      |
| `FLINT_AND_STEEL` | Eslabón y pedernal |

---

# 🌌 Dimensiones

```yaml
dimensions:
  shadow_realm:
    enabled: true
    world-name: "shadow_realm"
    environment: NORMAL
```

---

# 👑 Bosses de Dimensión

```yaml
boss-spawn-mode: SUMMONER

dimension-boss: shadow_overlord
```

---

# ⏳ Sistema de Countdown

```yaml
countdown-enabled: true
countdown-seconds: 600
countdown-action: KILL_ALL
```

## Acciones del Countdown

| Acción         | Efecto                     |
| -------------- | -------------------------- |
| `KILL_ALL`     | Mata a todos los jugadores |
| `TELEPORT_OUT` | Expulsa jugadores          |
| `EMPOWER_BOSS` | Cura y buffea al boss      |

---

# 🎨 Códigos de Color

```text
&a Verde
&c Rojo
&5 Morado
&l Negrita
&o Cursiva
&r Reset
```

---

# ❓ FAQ

## El portal no se activa

* Verifica el tamaño del frame
* Verifica los materiales
* Verifica el item de activación
* El interior debe ser aire

## La dimensión no se genera

* Requiere Paper 1.20+
* Requiere Java 17+

---

# 🚀 Roadmap

* Editor gráfico GUI
* Soporte para base de datos
* Sistema de niveles para mobs
* Progresión RPG
* Compatibilidad con PlaceholderAPI

---

# 📜 Licencia

MIT License

---

# ❤️ Créditos

Made for edumc_
discord: eduardo_mc.
eonix studios link:``` https://discord.gg/XbvxKhEN
```


