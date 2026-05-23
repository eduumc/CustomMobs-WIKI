# CustomMobs Plugin — Wiki en Español

> Versión 2.0 | Paper/Spigot 1.18–1.21 | Java 17+

---

## Índice

1. [Instalación](#instalación)
2. [Estructura de Archivos](#estructura-de-archivos)
3. [Comandos](#comandos)
4. [Permisos](#permisos)
5. [Crear un Mob Custom](#crear-un-mob-custom)
6. [Modos de IA](#modos-de-ia)
7. [Sistema de Fases](#sistema-de-fases)
8. [Habilidades](#habilidades)
9. [Sistema de Drops](#sistema-de-drops)
10. [Sistema de Spawn](#sistema-de-spawn)
11. [Sistema de Portales](#sistema-de-portales)
12. [Sistema de Dimensiones](#sistema-de-dimensiones)
13. [Sistema de Boss](#sistema-de-boss)
14. [Gestión por GUI](#gestión-por-gui)
15. [Multilenguaje](#multilenguaje)
16. [Notificador de Versiones](#notificador-de-versiones)
17. [Referencia de Colores](#referencia-de-colores)
18. [Preguntas Frecuentes](#preguntas-frecuentes)

---

## Instalación

1. Descarga el `.jar` más reciente desde [Releases](../../../releases/latest)
2. Colócalo en la carpeta `plugins/` de tu servidor
3. Inicia el servidor — los archivos de configuración se generan automáticamente
4. Edita los archivos en `plugins/CustomMobPlugin/` según necesites
5. Usa `/cm reload` para aplicar cambios sin reiniciar

**Requisitos:**
- Paper o Spigot 1.18 – 1.21.x
- Java 17+
- Paper 1.20+ requerido para dimensiones custom
- WorldEdit o FAWE opcional (para schematics)

---

## Estructura de Archivos

```
plugins/CustomMobPlugin/
├── config.yml                  ← Solo configuración global
├── mobs/
│   ├── forest_stalker.yml      ← Un archivo por mob
│   ├── shadow_overlord.yml
│   └── tu_mob.yml
├── portals/
│   └── shadow_realm_portal.yml
├── dimensions/
│   └── shadow_realm.yml
└── lang/
    ├── messages_es.yml
    └── messages_en.yml
```

**Cada mob tiene su propio archivo YAML** en la carpeta `mobs/`. El nombre del archivo (sin `.yml`) se convierte en el ID del mob.

---

## Comandos

Todos los comandos usan `/custommob` con alias `/cmob` y `/cm`.

| Comando | Descripción | Permiso |
|---|---|---|
| `/cm list` | Lista todos los mobs cargados | `custommobs.use` |
| `/cm spawn <id> [cantidad]` | Spawnea un mob en tu posición | `custommobs.spawn` |
| `/cm info <id>` | Muestra detalles del mob | `custommobs.info` |
| `/cm kill <id\|all>` | Elimina mobs custom | `custommobs.kill` |
| `/cm gui` | Abre el panel de gestión | `custommobs.gui` |
| `/cm dim <nombre>` | Teletransporta a una dimensión | `custommobs.admin` |
| `/cm dims` | Lista dimensiones y portales | `custommobs.use` |
| `/cm givesummoner <dim> [jugador]` | Da el item invocador de boss | `custommobs.admin` |
| `/cm givekey <portal> [jugador]` | Da la llave de activación del portal | `custommobs.givekey` |
| `/cm spawnboss <dim>` | Fuerza el spawn del boss | `custommobs.admin` |
| `/cm skipcooldown <jugador> <dim>` | Salta el cooldown de entrada | `custommobs.skipcooldown` |
| `/cm cooldown <dim>` | Revisa tu cooldown | `custommobs.use` |
| `/cm reload` | Recarga toda la configuración | `custommobs.admin` |

---

## Permisos

| Permiso | Descripción | Por defecto |
|---|---|---|
| `custommobs.use` | Acceso básico (list, dims, cooldown) | Todos |
| `custommobs.info` | Ver detalles de mobs | Todos |
| `custommobs.spawn` | Spawnear mobs con comandos | OP |
| `custommobs.kill` | Eliminar mobs custom | OP |
| `custommobs.gui` | Acceder al panel GUI | OP |
| `custommobs.givekey` | Dar llaves de portal | OP |
| `custommobs.skipcooldown` | Saltar cooldown de dimensión | OP |
| `custommobs.admin` | Acceso admin completo | OP |
| `custommobs.*` | Todos los permisos | OP |

---

## Crear un Mob Custom

### Desde la GUI (Recomendado)

1. Ejecuta `/cm gui`
2. Haz clic en **✚ Crear Mob**
3. Escribe el ID del mob (paso 1)
4. Haz clic en entidad base — navega por los huevos o escríbela manualmente (paso 2)
5. Escribe el nombre visual (paso 3)
6. El archivo se crea automáticamente en `mobs/<id>.yml`
7. Edita el resto de opciones desde la GUI

### Desde un archivo YAML

Crea un archivo en `plugins/CustomMobPlugin/mobs/tu_mob_id.yml`:

```yaml
enabled: true
display-name: "&cZombie de Fuego"
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
  scale: 1.0            # Requiere 1.20.5+

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
      custom-name: "&bDiamante de Fuego"
      lore:
        - "&7Dropeado por el Zombie de Fuego"
      enchantments:
        FIRE_PROTECTION: 2

ai:
  target: PLAYERS       # PLAYERS | ANIMALS | PLAYERS_AND_ANIMALS | ALL_MOBS | ALL
  flee-below-health: 0.0
  call-for-help: false
```

### Entidades Base Disponibles

Cualquier entidad hostil de Minecraft funciona como base. Las más comunes:
`ZOMBIE`, `SKELETON`, `SPIDER`, `CREEPER`, `BLAZE`, `WITHER_SKELETON`, `DROWNED`, `HUSK`, `STRAY`, `PILLAGER`, `VINDICATOR`, `EVOKER`, `PHANTOM`, `GHAST`, `HOGLIN`, `PIGLIN_BRUTE`, `ZOGLIN`

---

## Modos de IA

### BASIC
IA por defecto con estas mejoras:
- Tipo de objetivo configurable
- Comportamiento de huida cuando la vida está baja
- Llamar refuerzos (alerta a mobs cercanos del mismo tipo)

### ADVANCED
Todo lo de BASIC más:
- Sistema de fases con umbrales de vida
- Habilidades especiales con cooldown por fase

### EPIC
Todo lo de ADVANCED más:
- Modificadores de velocidad por fase
- Efectos de transición de fase (rayo, mensajes)
- Invocación de minions al cambiar de fase
- Mecánicas completas de boss

### Opciones de Target

| Valor | Ataca a |
|---|---|
| `PLAYERS` | Solo jugadores |
| `ANIMALS` | Animales pasivos |
| `PLAYERS_AND_ANIMALS` | Jugadores y animales |
| `ALL_MOBS` | Todo excepto jugadores |
| `ALL` | Absolutamente todo |

---

## Sistema de Fases

Las fases se activan cuando la vida del mob cae por debajo del umbral.

```
100% ──── Fase 1 ──── 65% ──── Fase 2 ──── 30% ──── Fase 3
          (normal)             (rápido)               (desesperado)
```

```yaml
ai:
  phases:
    - name: "Despertar"
      health-threshold: 1.0       # Activa desde 100% hasta el siguiente umbral
      ability-cooldown: 60        # Ticks entre habilidades
      movement-speed-modifier: 1.0
      abilities:
        - SHADOW_STRIKE
        - DARKNESS_AURA
      phase-message: "&5El boss despierta..."
      phase-lightning: false
      summon-on-phase: false

    - name: "Furia"
      health-threshold: 0.6       # Se activa al bajar del 60%
      ability-cooldown: 35
      movement-speed-modifier: 1.3
      abilities:
        - SHADOW_STRIKE
        - VOID_BOLT
      phase-message: "&c&l¡MODO FURIA!"
      phase-lightning: true
      summon-on-phase: true
```

---

## Habilidades

Las habilidades se definen en `config.yml` bajo `abilities:` y se referencian por nombre en las fases.

| Habilidad | Descripción |
|---|---|
| `FIREBALL_BURST` | Dispara múltiples bolas de fuego al objetivo |
| `FIRE_AURA` | Quema a todos los jugadores en un radio |
| `SPEED_BOOST` | Da efecto de velocidad al mob |
| `EXPLOSION` | Crea una explosión en la posición del mob |
| `SHADOW_STRIKE` | Golpe poderoso que ciega y aplica wither |
| `DARKNESS_AURA` | Ciega y ralentiza a jugadores cercanos |
| `VOID_BOLT` | Daña y levita al objetivo |
| `SUMMON_MINIONS` | Invoca mobs definidos en `ai.minion-mob` |
| `TELEPORT` | Se teletransporta detrás del objetivo |
| `SHADOW_NOVA` | Onda expansiva que empuja y daña |
| `HEAL` | Cura al mob un porcentaje de su vida máxima |

---

## Sistema de Drops

```yaml
drops:
  exp-min: 10
  exp-max: 30
  items:
    - material: DIAMOND
      amount-min: 1
      amount-max: 3
      chance: 0.25          # 0.0 = nunca | 1.0 = siempre
      custom-name: "&bDiamante Mágico"
      lore:
        - "&7Una gema especial"
      enchantments:
        SHARPNESS: 5
        UNBREAKING: 3
      # Tags especiales:
      portal-key: shadow_realm_portal    # Convierte el item en llave de portal
      dimension-summoner: shadow_realm   # Convierte el item en invocador de boss
```

> ⚠️ **Importante:** `chance` debe estar entre `0.0` y `1.0`. Usar `1` significa 100%, no 1%.

### Agregar Drops desde la GUI

En el panel de drops, sostén cualquier item en tu mano principal y haz clic en **+ Add Item from Hand**. El plugin preserva:
- Material
- Nombre custom
- Lore
- Encantamientos
- Tags NBT de llave de portal / invocador

---

## Sistema de Spawn

| Modo | Descripción |
|---|---|
| `NATURAL` | Spawnea periódicamente según bioma, hora y nivel de luz |
| `TIMED` | Spawnea en intervalos fijos sin importar condiciones |
| `COMMAND_ONLY` | Solo spawnea con el comando `/cm spawn` |

**Referencia de ticks:**

| Ticks | Tiempo |
|---|---|
| 200 | 10 segundos |
| 1200 | 1 minuto |
| 6000 | 5 minutos |
| 12000 | 10 minutos |
| 72000 | 1 hora |

---

## Sistema de Portales

Los portales son estructuras físicas en el mundo que teletransportan a dimensiones custom.

### Construir un Portal Manualmente

1. Construye el frame con el bloque configurado en `frame-material`
2. El interior debe ser exactamente `frame-width × frame-height` bloques de aire
3. El plugin detecta el frame automáticamente al colocar el último bloque
4. Haz clic derecho en el frame con la llave de portal para activarlo

**Estructura del frame (4×5 interior con BLACKSTONE):**
```
■ ■ ■ ■ ■ ■   ← fila superior (frame-width + 2)
■ · · · · ■
■ · · · · ■   ← frame-height = 5 filas interiores
■ · · · · ■
■ · · · · ■
■ · · · · ■
■ ■ ■ ■ ■ ■   ← fila inferior
```

### Configuración del Portal

```yaml
# portals/mi_portal.yml
enabled: true
dimension: mi_dimension

frame-material: BLACKSTONE
portal-material: PURPLE_STAINED_GLASS_PANE
frame-width: 4
frame-height: 5

# ITEM | AUTO | FLINT_AND_STEEL
activation: ITEM
igniter-portal-key: mi_portal   # ID de la llave requerida para activar
igniter-consume: true
frame-breakable: true            # ¿Los jugadores en supervivencia pueden romper el frame?

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

### Obtener una Llave de Portal

```
/cm givekey <portal_id> [jugador]
```

O configura un mob para que la dropee:
```yaml
drops:
  items:
    - material: ENDER_EYE
      chance: 0.1
      custom-name: "&5Llave del Portal"
      portal-key: shadow_realm_portal
```

---

## Sistema de Dimensiones

Las dimensiones custom son mundos de Minecraft separados con mobs exclusivos.

> **Requiere Paper 1.20+**

```yaml
# dimensions/mi_dimension.yml
enabled: true
world-name: "mi_dimension"
environment: NORMAL     # NORMAL | NETHER | THE_END
generator: ""           # Vacío para generación normal

exclusive-mobs:
  - mi_boss

# Bloquea spawns de mobs vanilla (solo tus mobs custom spawnean)
block-vanilla-spawns: true
kill-ender-dragon: true   # Solo para environment THE_END

gamerules:
  doMobSpawning: false
  doWeatherCycle: false
  doDaylightCycle: false
```

---

## Sistema de Boss

```yaml
boss-spawn-mode: SUMMONER   # AUTO | SUMMONER
dimension-boss: shadow_overlord
boss-spawn-offset-x: 0
boss-spawn-offset-y: 0
boss-spawn-offset-z: 10

# Temporizador de cuenta regresiva
countdown-enabled: true
countdown-seconds: 600
countdown-warning-seconds: [300, 60, 30, 10]
countdown-action: KILL_ALL  # KILL_ALL | TELEPORT_OUT | EMPOWER_BOSS

# Cooldown de entrada
cooldown-enabled: true
cooldown-minutes: 30
cooldown-message: "&cEspera &e{time} &cantes de entrar de nuevo."

# Post-boss
clear-dimension-on-boss-death: true
teleport-out-on-boss-death: false
teleport-delay-seconds: 30
```

| Acción del Countdown | Qué ocurre |
|---|---|
| `KILL_ALL` | Todos los jugadores en la dimensión mueren y son enviados de vuelta |
| `TELEPORT_OUT` | Los jugadores son teletransportados sin morir |
| `EMPOWER_BOSS` | El boss se cura al 100% y duplica su velocidad |

### Item Invocador

Si `boss-spawn-mode: SUMMONER`, los jugadores deben usar un item invocador dentro de la dimensión para invocar al boss. Configura el drop en el yml del mob:

```yaml
drops:
  items:
    - material: NETHER_STAR
      chance: 0.05
      custom-name: "&5&lInvocador del Vacío"
      dimension-summoner: shadow_realm
```

Obtén uno al instante con:
```
/cm givesummoner <dimension_id> [jugador]
```

---

## Gestión por GUI

Abre con `/cm gui`. Requiere el permiso `custommobs.gui`.

### Panel Principal
Muestra todos los mobs cargados como cabezas de jugador con estadísticas. Haz clic en una cabeza para gestionar ese mob. Haz clic en **✚ Crear Mob** para crear uno nuevo.

### Panel de Detalle del Mob
- **Spawnear** — Spawnea el mob en tu posición
- **Eliminar Vivos** — Elimina todos los vivos
- **Cambiar Nombre** — Edita el nombre visual (input por chat)
- **Editar Drops** — Abre el editor de drops
- **Cambiar Target** — Selecciona el tipo de objetivo de IA
- **Cambiar Armadura** — Asigna slots de equipo
- **Atributos** — Edita vida, daño, velocidad, armadura
- **AI Mode** — Cicla entre BASIC → ADVANCED → EPIC

### Editor de Drops
- Clic izquierdo en un drop para ajustar su chance (input por chat)
- Clic derecho en un drop para eliminarlo
- **+ Add Item from Hand** — Sostén un item y haz clic para agregarlo como drop, conservando todos los metadatos

### Editor de Armadura
- Haz clic en **← Poner item de mano** para cualquier slot mientras sostienes el item que quieres asignar
- Haz clic en **Limpiar** para quitar el item de un slot

### Selector de Entidades (Flujo de Creación)
Al crear un mob, hacer clic en el botón de entidad abre una cuadrícula paginada con todos los huevos de spawn. Haz clic en un huevo para seleccionar ese tipo de entidad, o haz clic en **✎ Escribir manualmente** para escribir el nombre en el chat.

---

## Multilenguaje

Configura el idioma en `config.yml`:
```yaml
settings:
  language: es   # es | en
```

Los archivos de idioma están en `plugins/CustomMobPlugin/lang/messages_es.yml` y se pueden editar libremente. El plugin copia los archivos predeterminados al iniciar por primera vez.

---

## Notificador de Versiones

El plugin verifica automáticamente GitHub al iniciar para encontrar nuevas versiones. Los jugadores OP y administradores reciben una notificación al conectarse si hay una actualización disponible.

Para desactivarlo:
```yaml
settings:
  check-updates: false
```

---

## Referencia de Colores

| Código | Color/Formato |
|---|---|
| `&0` | Negro |
| `&1` | Azul Oscuro |
| `&2` | Verde Oscuro |
| `&3` | Cian Oscuro |
| `&4` | Rojo Oscuro |
| `&5` | Morado Oscuro |
| `&6` | Dorado |
| `&7` | Gris |
| `&8` | Gris Oscuro |
| `&9` | Azul |
| `&a` | Verde |
| `&b` | Cian |
| `&c` | Rojo |
| `&d` | Rosa |
| `&e` | Amarillo |
| `&f` | Blanco |
| `&l` | **Negrita** |
| `&o` | *Cursiva* |
| `&n` | Subrayado |
| `&m` | Tachado |
| `&k` | Ofuscado |
| `&r` | Reset |

---

## Preguntas Frecuentes

**¿Por qué no se activa el portal?**
Verifica que las dimensiones del frame coincidan exactamente con `frame-width` y `frame-height`. El interior debe ser aire vacío. Activa `debug: true` en config y revisa la consola al hacer clic.

**¿Por qué el mob no ataca a los animales?**
Bukkit no tiene soporte nativo para que mobs hostiles ataquen animales. El plugin escanea objetivos cada 2 segundos. Asegúrate de que el animal esté dentro del `follow-range` del mob.

**¿Por qué el interior del portal no se llenó completamente?**
Este era un bug en versiones anteriores. Asegúrate de usar v2.0+. El interior ahora se llena completamente usando `setType(mat, false)` para evitar conexiones entre paneles de cristal.

**¿Puedo tener múltiples dimensiones?**
Sí. Agrega un `.yml` por dimensión en la carpeta `dimensions/` y uno por portal en `portals/`.

**El mob que creé desde la GUI no spawnea.**
Asegúrate de que la entidad base sea una entidad viva válida (ej: `ZOMBIE`, no `ITEM` ni `ARROW`). Revisa la consola para ver un mensaje de advertencia del validador de spawn.


**¿Cómo creo una dimensión plana?**
Deja `generator: ""` y configura `gamerules.doMobSpawning: false`. Los mundos planos reales requieren un plugin de gestión de mundos como Multiverse-Core.

Esta wiki fue hecha por edumc_
