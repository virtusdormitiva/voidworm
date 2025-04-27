# Guía Técnica para la Creación de la Entidad "Void Worm" en Minecraft Bedrock Edition

---

## I. Introducción

### Objetivo
Este documento proporciona una guía técnica exhaustiva destinada a la creación de un Add-On para Minecraft Bedrock Edition. El objetivo principal es introducir una entidad personalizada, el **"Void Worm" (Gusano del Vacío)**, inspirada en la criatura homónima del mod "Alex's Mobs" para la Edición Java de Minecraft. Se detallarán los pasos y componentes necesarios para replicar sus características visuales, estadísticas, comportamientos, sonidos y objetos soltados al morir, adaptándolos a las capacidades y limitaciones de la plataforma Bedrock.

### Audiencia y Propósito
Esta guía está diseñada para:
- Asistentes de inteligencia artificial avanzados capaces de generar los archivos de Paquete de Comportamiento (Behavior Pack - BP) y Paquete de Recursos (Resource Pack - RP) necesarios.
- Desarrolladores humanos con conocimientos técnicos en Add-Ons para Bedrock.

El propósito es servir como un plano técnico detallado para la generación de archivos `.mcpack` funcionales que implementen la entidad Void Worm.

---

## II. Alcance y Limitaciones

### Características Clave del Void Worm
1. **Apariencia**:
   - Modelo 3D y texturas alusivas al vacío.
2. **Estadísticas**:
   - Salud, daño y velocidad personalizables.
3. **Comportamiento**:
   - Hostilidad hacia jugadores.
   - Patrones de ataque cuerpo a cuerpo y a distancia.
   - Maniobras de portal (teleportación simulada).
   - Mecánica de división (simulada).
4. **Sonidos**:
   - Eventos de sonido para ambiente, daño, muerte y ataque.
5. **Botín**:
   - Mandíbulas y ojo del vacío al morir.
6. **Invocación**:
   - Excluye la aparición natural; invocable únicamente con un huevo generador personalizado.

### Limitaciones Técnicas en Bedrock
1. La segmentación detallada y mecánicas complejas deberán ser simplificadas.
2. Los recursos visuales y auditivos específicos deben ser creados externamente.
3. La mecánica de división será simulada mediante sensores de daño y eventos personalizados.

---

## III. Estructura del Add-On

### Roles de los Paquetes
1. **Behavior Pack (BP)**:
   - Define lógica y comportamiento.
2. **Resource Pack (RP)**:
   - Define apariencia visual y auditiva.

### Estructura Estándar de Carpetas
#### Behavior Pack (Ej: `sonho_void_worm_bp`)
```
sonho_void_worm_bp/
├── entities/
│   ├── void_worm.json          # Definición del comportamiento
│   └── void_crystal.json       # (Opcional) Proyectil
├── loot_tables/
│   └── entities/
│       └── void_worm.json      # Tabla de botín
├── manifest.json               # Metadatos del BP
└── pack_icon.png               # Icono del paquete (opcional)
```

#### Resource Pack (Ej: `sonho_void_worm_rp`)
```
sonho_void_worm_rp/
├── entity/
│   ├── void_worm.entity.json   # Definición visual
│   └── void_crystal.entity.json # (Opcional) Proyectil
├── models/
│   └── entity/
│       ├── void_worm.geo.json  # Modelo 3D
│       └── void_crystal.geo.json # (Opcional) Proyectil
├── textures/
│   ├── entity/
│   │   ├── void_worm.png       # Textura del gusano
│   │   └── void_crystal.png    # (Opcional) Textura del proyectil
│   └── items/
│       └── spawn_egg_void_worm.png # Textura del huevo generador
├── render_controllers/
│   ├── void_worm.render_controllers.json
│   └── void_crystal.render_controllers.json
├── animations/
│   ├── void_worm.animation.json
│   └── void_crystal.animation.json
├── animation_controllers/
│   ├── void_worm.animation_controllers.json
│   └── void_crystal.animation_controllers.json
├── sounds/
│   └── mob/
│       └── void_worm/
│           ├── ambient1.ogg
│           └── hurt1.ogg
├── texts/
│   ├── en_US.lang
│   └── es_ES.lang
├── sounds.json
├── sound_definitions.json
├── textures/item_texture.json
├── manifest.json
└── pack_icon.png
```

---

## IV. Implementación del Behavior Pack

### Archivo de Definición de Entidad (`entities/void_worm.json`)
Define el comportamiento base del Void Worm, incluyendo:
- Salud: `160 HP`.
- Ataques cuerpo a cuerpo y a distancia.
- Simulación de maniobras de portal (teleportación).
- Simulación de división al recibir daño.

### Archivo de Tabla de Botín (`loot_tables/entities/void_worm.json`)
Define los objetos soltados:
- **Mandíbulas del Vacío** (`sonho:void_mandible`).
- **Ojo del Vacío** (`sonho:void_eye`).

---

## V. Implementación del Resource Pack

### Archivo de Entidad Visual (`entity/void_worm.entity.json`)
Vincula:
- Modelo 3D (`void_worm.geo.json`).
- Textura principal (`void_worm.png`).
- Animaciones (`void_worm.animation.json`).
- Configuración del huevo generador.

### Modelo 3D y Textura
- **Modelo**: Simplificado o segmentado, creado con Blockbench.
- **Textura**: Colores alusivos al vacío (oscuros, morados o negros).

### Animaciones
Define animaciones para:
- Movimiento.
- Ataque cuerpo a cuerpo.
- Ataque a distancia.
- Muerte.

### Sonidos
Archivos de audio (`.ogg`) para:
- Ambiente (`ambient1.ogg`).
- Daño (`hurt1.ogg`).
- Muerte (`death1.ogg`).
- Ataques cuerpo a cuerpo y a distancia.

---

## VI. Creación del Huevo Generador Personalizado

1. **Definición en Behavior Pack**:
   - `is_spawnable: false` (evita aparición natural).
   - `is_summonable: true` (permite invocación con huevo).

2. **Configuración en Resource Pack**:
   - Método 1: Colores estándar (`base_color`, `overlay_color`).
   - Método 2: Textura personalizada (`spawn_egg_void_worm.png`).

3. **Definición en Archivos de Idioma**:
   - `entity.sonho:void_worm.name=Void Worm`.
   - `item.spawn_egg.entity.sonho:void_worm.name=Spawn Void Worm`.

---

## VII. Empaquetado y Pruebas

1. **Creación de Archivos `.mcpack`**:
   - Comprimir el contenido de las carpetas BP y RP como archivos `.zip` y renombrarlos a `.mcpack`.

2. **Instalación**:
   - Importar los paquetes a Minecraft Bedrock haciendo doble clic en los archivos `.mcpack`.

3. **Activación**:
   - Activar los paquetes en la configuración del mundo.

4. **Pruebas**:
   - Invocar la entidad con el comando `/summon sonho:void_worm` o el huevo generador.
   - Verificar comportamiento, ataques, división, y botín.

---

## VIII. Consideraciones Finales

### Limitaciones de Bedrock
- La segmentación y mecánicas complejas son simuladas usando componentes JSON.
- Los recursos visuales y auditivos deben obtenerse o crearse externamente.

### Posibles Expansiones Futuras
1. Crear ítems funcionales basados en el botín.
2. Implementar recetas de crafteo para el trofeo y el pico.
3. Mejorar la IA con funciones avanzadas o scripting.

Esta guía sirve como un plano técnico para la creación de una entidad funcional en Minecraft Bedrock Edition, adaptando las mecánicas del Void Worm a las capacidades de la plataforma.
