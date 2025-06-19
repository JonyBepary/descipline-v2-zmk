# ZMK-v2 Firmware for Descipline V2 Keyboard

A comprehensive ZMK (Zephyr Mechanical Keyboard) firmware implementation for the Descipline V2 65% keyboard, featuring advanced ergonomic optimizations, clean typing experience, and intelligent layer management.

## Table of Contents

- [Project Overview](#project-overview)
- [Hardware Specifications](#hardware-specifications)
- [Keymap Layers](#keymap-layers)
- [Ergonomic Features](#ergonomic-features)
  - [Clean Home Row Typing](#clean-home-row-typing)
  - [Thumb-Based Layer Access](#thumb-based-layer-access)
  - [Clean Typing Experience](#clean-typing-experience)
  - [Advanced Behaviors](#advanced-behaviors)
- [Pin Configuration](#pin-configuration)
- [Build Instructions](#build-instructions)
- [Flash Instructions](#flash-instructions)
- [Configuration Files](#configuration-files)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## Project Overview

ZMK-v2 is a modern, feature-rich firmware for the Descipline V2 keyboard that prioritizes clean typing and ergonomic efficiency. Built on the ZMK firmware framework, it provides wireless connectivity, advanced key behaviors, and a carefully designed layer system optimized for programming and productivity workflows with uninterrupted home row typing.

### Key Features

- **6 Specialized Layers**: Default QWERTY, Function, Navigation, Media, Bluetooth, and Symbol layers
- **Clean Home Row Typing**: Pure letter input without interference from modifiers
- **Thumb-Based Layer Access**: Efficient layer switching without leaving home position
- **Enhanced Utility Organization**: Comprehensive function clustering with intuitive IJKL arrow diamond pattern
- **Clean F-Key Access**: Uncluttered left side for direct function key usage
- **Logical Grouping Strategy**: Navigation, system, and productivity utilities clustered for workflow efficiency
- **Wireless Connectivity**: Bluetooth with multi-device support
- **Advanced Behaviors**: Tap-dance, sticky keys, and custom macros
- **Optimized Symbol Layout**: Logical grouping of symbols and numbers

## Hardware Specifications

### Keyboard Details
- **Model**: Descipline V2
- **Layout**: 65% ANSI layout
- **Matrix**: 5x15 (5 rows, 15 columns)
- **Microcontroller**: Nice!Nano v2 (nRF52840)
- **Connectivity**: Wireless (Bluetooth 5.0) and USB-C
- **Diode Direction**: COL2ROW
- **Key Count**: 68 keys

### Controller Specifications
- **MCU**: Nordic nRF52840
- **Architecture**: ARM Cortex-M4F
- **Flash**: 1MB
- **RAM**: 256KB
- **Bluetooth**: 5.0/5.1/5.2 compatible
- **USB**: USB 2.0 Full Speed

## Keymap Layers

The firmware implements 6 carefully designed layers, each optimized for specific use cases:

### Layer 0: DEFAULT (QWERTY Base Layer)

The foundation layer with clean home row keys for uninterrupted typing.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│ ESC │  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │  0  │  -  │  =  │   BKSP   │ DEL │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│  TAB   │  Q  │  W  │  E  │  R  │  T  │  Y  │  U  │  I  │  O  │  P  │  [  │  ]  │   \   │PGUP │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│CAPS/FN   │  A  │  S  │  D  │  F  │  G  │  H  │  J  │  K  │  L  │  ;  │  '  │   ENTER   │PGDN │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│  LSHIFT  │  Z   │  X   │  C  │  V  │  B  │  N  │  M  │  ,  │  .  │  /  │RSHFT│   UP    │ MOD │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│LCTL│ LGUI │LGUI│  LALT   │       SYM/SPACE             │NAV/SPC │  FN  │RCTL│LEFT │DOWN │RGHT │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Clean Home Row Keys**:
- **A, S, D, F**: Pure letter input without modifier interference
- **J, K, L, ;**: Pure letter input without modifier interference
- **Modifiers**: Located in traditional positions (Ctrl, Alt, GUI, Shift)

### Layer 1: FN (Function Keys & Utility Controls)

Enhanced function layer with logical utility organization - clean F-key focus on the left, comprehensive utility grouping on the right.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│  `  │ F1  │ F2  │ F3  │ F4  │ F5  │ F6  │ F7  │ F8  │ F9  │ F10 │ F11 │ F12 │   DEL    │ INS │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │     │     │     │     │     │     │     │ UP  │HOME │PGUP │PSCRN│SCLK │ PAUSE │EMAIL│
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │     │     │     │     │     │     │LEFT │DOWN │RGHT │ DEL │ END │    END    │SAVE │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │C_PRV │C_PP  │C_NXT│     │     │     │     │PGDN │     │     │     │  VOL+   │  BT │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │                             │        │      │    │PREV │VOL- │NEXT │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Enhanced FN Layer Organization**:

**Left Side - Clean F-Key Focus**:
- **Function Keys**: F1-F12 positioned cleanly across the top for unobstructed access
- **Transparent Positions**: Clean layout without utility clutter for focused F-key usage
- **Media Controls**: Previous/Play-Pause/Next positioned on the left for media management

**Right Side - Logical Utility Grouping**:
- **Arrow Diamond Cluster**: IJKL pattern - I(UP), J(LEFT), K(DOWN), L(RIGHT) in intuitive diamond formation for directional navigation
- **Navigation Utilities**: HOME, DELETE, PAGE UP, PAGE DOWN, INSERT strategically positioned
- **System Utilities**: PRINT SCREEN, SCROLL LOCK, PAUSE grouped together for system functions
- **Productivity Keys**: EMAIL and SAVE macros positioned for quick access
- **Layer Access**: Bluetooth layer activation for wireless management

**Grouping Logic Benefits**:
- **Intuitive Navigation**: Arrow keys form natural diamond pattern for muscle memory
- **Function Clustering**: Similar utilities grouped together for improved workflow efficiency
- **Clean Separation**: F-keys isolated from utilities to prevent accidental activation
- **Ergonomic Access**: High-use utilities positioned for comfortable thumb and finger reach

### Layer 2: NAV (Navigation & Text Editing)

Optimized navigation with IJKL arrow keys and text editing shortcuts.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│     │     │     │     │     │     │     │     │     │     │     │     │     │   DEL    │     │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │     │     │UNDO │REDO │     │     │HOME │ UP  │ END │     │     │     │       │     │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │     │     │     │     │     │     │LEFT │DOWN │RGHT │     │     │           │     │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │      │ CUT  │COPY │PASTE│     │     │     │PGDN │     │     │     │         │     │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │           SPACE             │        │      │    │     │     │     │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Navigation Features**:
- **IJKL**: IJKL arrow keys (I=Up, J=Left, K=Down, L=Right)
- **Home/End/PgUp/PgDn**: Strategic positioning for easy access
- **Undo/Redo**: Ctrl+Z/Ctrl+Y for quick text editing
- **Cut/Copy/Paste**: Standard editing shortcuts

### Layer 3: MEDIA (Media & System Controls)

Media playback and volume controls.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│     │     │     │     │     │     │     │     │     │     │     │     │     │          │     │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │     │     │     │     │     │     │     │     │     │     │     │     │       │     │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │     │     │     │     │     │     │     │     │     │     │     │           │     │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │ MUTE │ VOL- │VOL+ │     │     │     │     │     │     │     │     │         │     │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │                             │        │      │    │PREV │PLAY │NEXT │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

### Layer 4: BT (Bluetooth Management)

Bluetooth device switching and system reset functions.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│BTCLR│ BT0 │ BT1 │ BT2 │ BT3 │ BT4 │     │     │     │     │     │     │     │          │     │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│OUT_TOG │ USB │ BLE │     │     │     │     │     │     │     │     │     │     │       │     │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │     │     │     │     │     │     │     │     │     │     │     │           │     │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│BOOTLOADER│RESET │      │     │     │     │     │     │     │     │     │     │         │     │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │           SPACE             │        │      │    │     │     │     │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Bluetooth Features**:
- **BT0-BT4**: Connect to Bluetooth devices 0-4
- **BTCLR**: Clear all Bluetooth bonds
- **OUT_TOG**: Toggle between USB and Bluetooth output
- **USB/BLE**: Force specific output mode
- **BOOTLOADER**: Enter bootloader mode for flashing
- **RESET**: Soft reset the keyboard

### Layer 5: SYM (Symbol Layer)

Optimized symbol and number layout for programming and mathematical input.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│  `  │  !  │  @  │  #  │  $  │  %  │  ^  │  &  │  *  │  (  │  )  │  _  │  +  │          │     │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │  0  │  [  │  ]  │   \   │     │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │  !  │  @  │  #  │  $  │  %  │  ^  │  &  │  *  │  (  │  )  │  '  │           │     │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │  ~   │  |   │  {  │  }  │     │     │  _  │  +  │  -  │  =  │     │         │     │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │                             │  SPACE │      │    │     │     │     │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Symbol Organization**:
- **Top Row**: Mathematical and logical operators
- **Number Row**: Easy access to numbers 1-0
- **Symbol Row**: Programming symbols and brackets
- **Bottom Row**: Additional symbols and operators

## Ergonomic Features

### Clean Home Row Typing

The home row keys provide a clean, uninterrupted typing experience:

- **Pure Letter Input**: A, S, D, F, J, K, L, ; keys provide direct letter input without hold-tap behavior
- **No Modifier Interference**: Home row keys respond instantly without timing delays
- **Traditional Modifiers**: Ctrl, Alt, GUI, and Shift remain in their standard positions
- **Comfortable Typing**: No accidental modifier activation during fast typing

### Thumb-Based Layer Access

Efficient layer switching using thumb keys:

- **Left Thumb**: Symbol layer activation with space fallback
- **Right Thumb**: Navigation layer activation with space fallback
- **Balanced Hold-Tap**: 175ms timing optimized for natural typing rhythm

### Intelligent Layer Organization

The keymap features enhanced logical grouping and clustering of functions across layers:

**FN Layer - Comprehensive Utility Organization**:
- **Clean Left Focus**: F-keys positioned without utility interference for direct access
- **Right-Side Clustering**: All utilities logically grouped together for improved muscle memory
- **Arrow Diamond Pattern**: IJKL pattern - I(UP), J(LEFT), K(DOWN), L(RIGHT) arranged in intuitive diamond formation
- **Function Clusters**: Navigation utilities (HOME, DELETE, PAGE UP/DOWN, INSERT) grouped together
- **System Clusters**: PRINT SCREEN, SCROLL LOCK, PAUSE grouped for system functions
- **Productivity Access**: EMAIL and SAVE macros strategically positioned for workflow efficiency

**Cross-Layer Consistency**:
- **Symbol Layer**: Numbers on home row with logical symbol grouping for programming efficiency
- **NAV Layer**: IJKL arrow keys with strategic text editing shortcuts
- **Specialized Layers**: Dedicated media controls and Bluetooth management

**Ergonomic Benefits**:
- **Reduced Cognitive Load**: Similar functions clustered together reduce mental mapping
- **Improved Muscle Memory**: Consistent grouping patterns across similar functions
- **Efficient Workflows**: Logical positioning minimizes hand movement and finger travel

### FN Layer Grouping Logic

The enhanced FN layer organization follows intuitive grouping principles:

**Arrow Key Diamond Pattern**:
- **Natural Formation**: IJKL pattern - I(UP), J(LEFT), K(DOWN), L(RIGHT) positioned in diamond shape matching directional logic
- **Muscle Memory**: Intuitive finger positioning mirrors physical directional movement
- **Quick Access**: Clustered together for rapid directional navigation without hand repositioning

**Utility Clustering Strategy**:
- **Navigation Group**: HOME, DELETE, PAGE UP/DOWN, INSERT positioned together for document navigation
- **System Group**: PRINT SCREEN, SCROLL LOCK, PAUSE clustered for system-level functions
- **Productivity Group**: EMAIL and SAVE macros strategically placed for workflow efficiency
- **Clean Separation**: F-keys isolated on left side to prevent accidental utility activation

**Ergonomic Advantages**:
- **Reduced Hand Movement**: Similar functions within comfortable finger reach
- **Improved Efficiency**: Logical grouping reduces time spent searching for functions
- **Enhanced Muscle Memory**: Consistent clustering patterns accelerate learning and usage
- **Workflow Optimization**: Related functions positioned to support common task sequences

### Clean Typing Experience

The keymap prioritizes a pure typing experience with enhanced organizational benefits:

- **Immediate Response**: Home row keys (A, S, D, F, J, K, L, ;) provide instant letter input
- **No Timing Delays**: Zero latency on home row letter keys for fast, fluid typing
- **Reduced Complexity**: Eliminates potential conflicts between letters and modifiers
- **Traditional Layout**: Modifiers remain in familiar positions for muscle memory
- **Enhanced Function Access**: Logical clustering improves utility access without disrupting typing flow
- **Workflow Integration**: Strategic function grouping supports seamless transitions between typing and navigation

### Advanced Behaviors

#### Layer-Tap for Thumb Keys
- **Left Thumb**: Symbol layer access with space fallback
- **Right Thumb**: Navigation layer access with space fallback
- **Optimized Timing**: 175ms hold threshold with 125ms quick-tap for natural typing rhythm

#### Tap-Dance Capabilities
- **CAPS Key**: Single tap for FN layer, double tap for CAPS LOCK
- **Optimized Timing**: 200ms for comfortable double-tap recognition

#### Sticky Keys
- **Quick Release**: 1000ms timeout with immediate release on next key
- **Modifier Ignore**: Prevents interference with typing flow

#### Custom Macros
- **Email Macro**: Quick email address insertion
- **Save Macro**: Ctrl+S shortcut for rapid file saving

## Pin Configuration

### Matrix Configuration

The keyboard uses a 5x15 matrix with COL2ROW diode direction.

#### Row Pins (5 rows)
| Row | Pin | GPIO | Function |
|-----|-----|------|----------|
| 0   | D4  | P0.22 | Row 0 |
| 1   | D12 | P1.02 | Row 1 |
| 2   | D0  | P0.08 | Row 2 |
| 3   | D6  | P1.00 | Row 3 |
| 4   | D5  | P0.24 | Row 4 |

#### Column Pins (15 columns)
| Col | Pin | GPIO | Function |
|-----|-----|------|----------|
| 0   | D13 | P1.07 | Col 0 |
| 1   | D3  | P0.20 | Col 1 |
| 2   | D1  | P0.06 | Col 2 |
| 3   | D11 | P1.01 | Col 3 |
| 4   | D7  | P0.11 | Col 4 |
| 5   | D8  | P1.04 | Col 5 |
| 6   | D9  | P1.06 | Col 6 |
| 7   | D21 | P0.31 | Col 7 |
| 8   | D20 | P0.29 | Col 8 |
| 9   | D19 | P0.02 | Col 9 |
| 10  | D18 | P1.15 | Col 10 |
| 11  | D15 | P1.13 | Col 11 |
| 12  | D14 | P1.11 | Col 12 |
| 13  | D16 | P0.10 | Col 13 |
| 14  | D10 | P0.09 | Col 14 |

### Nice!Nano v2 Pinout

#### Left Side Connections
| Pin | Label | GPIO | Keyboard Function |
|-----|-------|------|-------------------|
| 1   | GND   | -    | Ground |
| 2   | D1    | P0.06 | Col 2 |
| 3   | D0    | P0.08 | Row 2 |
| 4   | GND   | -    | Ground |
| 5   | GND   | -    | Ground |
| 6   | D2    | P0.17 | Unused |
| 7   | D3    | P0.20 | Col 1 |
| 8   | D4    | P0.22 | Row 0 |
| 9   | D5    | P0.24 | Row 4 |
| 10  | D6    | P1.00 | Row 3 |
| 11  | D7    | P0.11 | Col 4 |
| 12  | D8    | P1.04 | Col 5 |
| 13  | D9    | P1.06 | Col 6 |

#### Right Side Connections
| Pin | Label | GPIO | Keyboard Function |
|-----|-------|------|-------------------|
| 1   | B+    | -    | Battery Positive |
| 2   | B+    | -    | Battery Positive |
| 3   | GND   | -    | Ground |
| 4   | RST   | -    | Reset |
| 5   | 3.3V  | -    | 3.3V Power |
| 6   | D21   | P0.31 | Col 7 |
| 7   | D20   | P0.29 | Col 8 |
| 8   | D19   | P0.02 | Col 9 |
| 9   | D18   | P1.15 | Col 10 |
| 10  | D15   | P1.13 | Col 11 |
| 11  | D14   | P1.11 | Col 12 |
| 12  | D16   | P0.10 | Col 13 |
| 13  | D10   | P0.09 | Col 14 |

#### Middle Connections
| Pin | Label | GPIO | Keyboard Function |
|-----|-------|------|-------------------|
| 1   | D11   | P1.01 | Col 3 |
| 2   | D12   | P1.02 | Row 1 |
| 3   | D13   | P1.07 | Col 0 |

## Build Instructions

### Prerequisites

1. **Install ZMK Development Environment**:
   ```bash
   # Install West (Zephyr's meta-tool)
   pip3 install --user -U west

   # Initialize ZMK workspace
   west init -l config
   west update

   # Install Zephyr SDK
   west zephyr-export
   ```

2. **Install Build Tools**:
   ```bash
   # Ubuntu/Debian
   sudo apt install --no-install-recommends git cmake ninja-build gperf \
     ccache dfu-util device-tree-compiler wget \
     python3-dev python3-pip python3-setuptools python3-tk python3-wheel \
     xz-utils file make gcc gcc-multilib g++-multilib libsdl2-dev

   # macOS
   brew install cmake ninja gperf python3 ccache qemu dtc
   ```

### Building the Firmware

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-username/zmk-v2.git
   cd zmk-v2
   ```

2. **Build for Nice!Nano v2**:
   ```bash
   west build -d build/descipline_rf -b nice_nano_v2 -- -DSHIELD=descipline_rf
   ```

3. **Build Output**:
   The firmware file will be generated at:
   ```
   build/descipline_rf/zephyr/zmk.uf2
   ```

### Build Configuration

The build is configured via [`build.yaml`](build.yaml):

```yaml
include:
  - board: nice_nano_v2
    shield: descipline_rf
```

## Flash Instructions

### Method 1: UF2 Bootloader (Recommended)

1. **Enter Bootloader Mode**:
   - Double-tap the reset button on the Nice!Nano
   - The controller will appear as a USB drive named "NICENANO"

2. **Flash Firmware**:
   - Copy `zmk.uf2` to the NICENANO drive
   - The controller will automatically reboot with new firmware

### Method 2: Via Bluetooth Layer

1. **Access Bootloader**:
   - Activate BT layer (Layer 4)
   - Press the BOOTLOADER key (bottom-left position)

2. **Flash via UF2**:
   - Follow Method 1 steps 2

### Verification

After flashing:
1. The keyboard should reconnect automatically
2. Test basic typing functionality
3. Verify layer switching works correctly
4. Check Bluetooth connectivity if applicable

## Configuration Files

### Core Configuration

| File | Purpose |
|------|---------|
| [`descipline_rf.keymap`](boards/shields/descipline_rf/descipline_rf.keymap) | Main keymap definition |
| [`descipline_rf.overlay`](boards/shields/descipline_rf/descipline_rf.overlay) | Hardware configuration |
| [`descipline_rf-layouts.dtsi`](boards/shields/descipline_rf/descipline_rf-layouts.dtsi) | Physical layout definition |
| [`Kconfig.shield`](boards/shields/descipline_rf/Kconfig.shield) | Shield configuration |
| [`Kconfig.defconfig`](boards/shields/descipline_rf/Kconfig.defconfig) | Default configuration |

### Build System

| File | Purpose |
|------|---------|
| [`build.yaml`](build.yaml) | GitHub Actions build matrix |
| [`west.yml`](config/west.yml) | West manifest for dependencies |
| [`module.yml`](zephyr/module.yml) | Zephyr module configuration |

### Hardware Specifications

- **Matrix Transform**: 5x15 matrix configuration
- **Physical Layout**: 65% ANSI layout with 68 keys
- **Diode Direction**: COL2ROW scanning
- **Key Spacing**: Standard 100-unit grid spacing

## Troubleshooting

### Common Issues

#### 1. Build Failures

**Issue**: Build fails with dependency errors
```bash
west build -d build/descipline_rf -b nice_nano_v2 -- -DSHIELD=descipline_rf
```

**Solution**:
```bash
# Update dependencies
west update

# Clean build directory
rm -rf build/
west build -d build/descipline_rf -b nice_nano_v2 -- -DSHIELD=descipline_rf
```

#### 2. Keyboard Not Responding

**Issue**: Keys not registering after flash

**Solution**:
1. Check wiring connections against pin configuration
2. Verify matrix transform matches physical layout
3. Reset to bootloader and reflash firmware

#### 3. Bluetooth Connection Issues

**Issue**: Cannot connect or frequent disconnections

**Solution**:
1. Clear Bluetooth bonds: Access BT layer → BTCLR
2. Reset keyboard: Access BT layer → RESET
3. Re-pair device from scratch

#### 4. Layer Switching Problems

**Issue**: Layers not activating correctly

**Solution**:
1. Check layer-tap timing configuration
2. Verify thumb key bindings in keymap
3. Test with simple momentary layer switch first

### Debug Mode

Enable debug logging by adding to configuration:

```c
CONFIG_ZMK_USB_LOGGING=y
CONFIG_LOG_DEFAULT_LEVEL=4
```

### Factory Reset

To restore default settings:
1. Access BT layer (Layer 4)
2. Press BOOTLOADER + RESET simultaneously
3. Flash original firmware

## Advanced Customization

### Modifying Behaviors

Edit behavior parameters in [`descipline_rf.keymap`](boards/shields/descipline_rf/descipline_rf.keymap):

**Layer-Tap Behavior for Thumb Keys**:
```c
lt_spc: layer_tap_space {
    tapping-term-ms = <175>;      // Hold threshold for layer access
    quick-tap-ms = <125>;         // Quick tap threshold for space
    flavor = "balanced";          // Timing behavior
};
```

**Tap-Dance for CAPS/FN Key**:
```c
td_caps: tap_dance_caps {
    tapping-term-ms = <200>;      // Double-tap timing
    bindings = <&mo FN>, <&kp CAPS>;  // Single tap = FN layer, double tap = CAPS
};
```

### Adding Custom Macros

Define new macros in the macros section:

```c
macros {
    your_macro: your_macro {
        label = "YOUR_MACRO";
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings = <&macro_tap &kp Y &kp O &kp U &kp R &kp SPACE &kp T &kp E &kp X &kp T>;
    };
};
```

### Layer Customization

Add or modify layers by:
1. Define layer constant: `#define CUSTOM 6`
2. Add layer to keymap with appropriate bindings
3. Reference layer in key bindings: `&mo CUSTOM`

## Contributing

### Development Workflow

1. **Fork the Repository**
2. **Create Feature Branch**:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make Changes**:
   - Edit keymap configurations
   - Test thoroughly
   - Document changes

4. **Submit Pull Request**:
   - Describe changes clearly
   - Include testing results
   - Reference related issues

### Testing Guidelines

Before submitting changes:
1. **Build Test**: Ensure firmware builds successfully
2. **Flash Test**: Verify firmware flashes and keyboard functions
3. **Layer Test**: Test all layer activations and key functions
4. **Timing Test**: Verify home row modifiers work correctly
5. **Bluetooth Test**: Test wireless connectivity (if applicable)

### Code Style

- Follow existing indentation and formatting
- Comment complex behavior configurations
- Use descriptive names for custom behaviors
- Group related settings together

## License

This project is licensed under the MIT License - see the ZMK Contributors license for details.

## Acknowledgments

- **ZMK Contributors**: For the excellent ZMK firmware framework
- **Discipline V2 by coseyfannitutti**: For the exceptional hardware specifications and innovative keyboard design - [GitHub Repository](https://github.com/coseyfannitutti/discipline)
- **Nice!Nano V2**: For the excellent wireless controller platform
## Support

For issues and questions:
1. No support will be provided for this firmware.
2. Please refer to the [ZMK Discord](https://discord.gg/zmk) for community support.
3. For hardware-related issues, refer to the [Discipline V2 GitHub](https://github.com/coseyfannitutti/discipline)

---

**Note**: This documentation is for ZMK-v2 firmware specifically designed for the Descipline V2 keyboard with Nice!Nano v2 or nrf promicro controller. This implementation prioritizes clean home row typing without modifiers for an uninterrupted typing experience. For other keyboards or controllers, configuration details may differ.
