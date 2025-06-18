# ZMK-v2 Firmware for Descipline V2 Keyboard

A comprehensive ZMK (Zephyr Mechanical Keyboard) firmware implementation for the Descipline V2 65% keyboard, featuring advanced ergonomic optimizations, home row modifiers, and intelligent layer management.

## Table of Contents

- [Project Overview](#project-overview)
- [Hardware Specifications](#hardware-specifications)
- [Keymap Layers](#keymap-layers)
- [Ergonomic Features](#ergonomic-features)
- [Pin Configuration](#pin-configuration)
- [Build Instructions](#build-instructions)
- [Flash Instructions](#flash-instructions)
- [Configuration Files](#configuration-files)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)

## Project Overview

ZMK-v2 is a modern, feature-rich firmware for the Descipline V2 keyboard that prioritizes ergonomics and efficiency. Built on the ZMK firmware framework, it provides wireless connectivity, advanced key behaviors, and a carefully designed layer system optimized for programming and productivity workflows.

### Key Features

- **6 Specialized Layers**: Default QWERTY, Function, Navigation, Media, Bluetooth, and Symbol layers
- **Home Row Modifiers**: Ergonomic modifier placement reducing finger stretching
- **Thumb-Based Layer Access**: Efficient layer switching without leaving home position
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

The foundation layer with home row modifiers for ergonomic typing.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│ ESC │  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │  9  │  0  │  -  │  =  │   BKSP   │ DEL │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│  TAB   │  Q  │  W  │  E  │  R  │  T  │  Y  │  U  │  I  │  O  │  P  │  [  │  ]  │   \   │PGUP │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│CAPS/FN   │A/CTL│S/ALT│D/GUI│F/SHF│  G  │  H  │J/SHF│K/GUI│L/ALT│;/CTL│  '  │   ENTER   │PGDN │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│  LSHIFT  │   Z  │  X   │  C  │  V  │  B  │  N  │  M  │  ,  │  .  │  /  │RSHFT│   UP    │ MOD │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│LCTL│ LGUI │LALT│         │       SYM/SPACE             │NAV/SPC │  FN  │RCTL│LEFT │DOWN │RGHT │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Home Row Modifiers**:
- **A**: Control (hold) / A (tap)
- **S**: Alt (hold) / S (tap)
- **D**: GUI/Super (hold) / D (tap)
- **F**: Shift (hold) / F (tap)
- **J**: Shift (hold) / J (tap)
- **K**: GUI/Super (hold) / K (tap)
- **L**: Alt (hold) / L (tap)
- **;**: Control (hold) / ; (tap)

### Layer 1: FN (Function Keys & System Controls)

Function keys, navigation arrows, and system controls.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│  `  │ F1  │ F2  │ F3  │ F4  │ F5  │ F6  │ F7  │ F8  │ F9  │ F10 │ F11 │ F12 │   DEL    │ INS │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │     │ UP  │     │     │     │     │     │ INS │HOME │PGUP │PSCRN│SCLK │ PAUSE │HOME │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │LEFT │DOWN │RGHT │     │     │     │     │ DEL │END  │PGDN │     │           │END  │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │C_PRV │C_PP  │C_NXT│     │     │     │EMAIL│SAVE │     │     │     │  VOL+   │  BT │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │                             │        │      │    │PREV │VOL- │NEXT │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

### Layer 2: NAV (Navigation & Text Editing)

Optimized navigation with HJKL arrow keys and text editing shortcuts.

```
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┬──────────┬─────┐
│     │     │     │     │     │     │     │     │     │     │     │     │     │   DEL    │     │
├─────┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬──┴──┬───────┼─────┤
│        │     │     │UNDO │REDO │     │     │HOME │PGUP │END  │     │     │     │       │     │
├────────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴───────┼─────┤
│          │     │     │     │     │     │LEFT │DOWN │ UP  │RGHT │     │     │           │     │
├──────────┼─────┴┬────┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬───┴─┬─────────┬─────┤
│          │      │ CUT  │COPY │PASTE│     │     │     │PGDN │     │     │     │         │     │
├────┬─────┴┬────┬┴─────┴──┬──┴─────┴─────┴─────┴─────┴──┬──┴─────┼─────┴┬────┬─────┬─────┬─────┤
│    │      │    │         │           SPACE             │        │      │    │     │     │     │
└────┴──────┴────┴─────────┴─────────────────────────────┴────────┴──────┴────┴─────┴─────┴─────┘
```

**Navigation Features**:
- **HJKL**: Vi-style arrow keys (H=Left, J=Down, K=Up, L=Right)
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
│          │ MUTE │VOL-  │VOL+ │     │     │     │     │     │     │     │     │         │     │
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

### Home Row Modifiers

Home row modifiers reduce finger stretching and improve typing ergonomics:

- **Left Hand**: Ctrl(A), Alt(S), GUI(D), Shift(F)
- **Right Hand**: Shift(J), GUI(K), Alt(L), Ctrl(;)
- **Timing**: 175ms tapping term with 125ms quick-tap
- **Idle Requirement**: 150ms prior idle to prevent accidental activation

### Thumb-Based Layer Access

Efficient layer switching using thumb keys:

- **Left Thumb**: Symbol layer activation with space fallback
- **Right Thumb**: Navigation layer activation with space fallback
- **Balanced Hold-Tap**: 175ms timing optimized for natural typing rhythm

### Advanced Behaviors

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

#### 3. Home Row Modifiers Too Sensitive

**Issue**: Modifiers activating during normal typing

**Solution**: Adjust timing in keymap:
```c
tapping-term-ms = <200>;        // Increase from 175
require-prior-idle-ms = <200>;  // Increase from 150
```

#### 4. Bluetooth Connection Issues

**Issue**: Cannot connect or frequent disconnections

**Solution**:
1. Clear Bluetooth bonds: Access BT layer → BTCLR
2. Reset keyboard: Access BT layer → RESET
3. Re-pair device from scratch

#### 5. Layer Switching Problems

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

```c
hm: homerow_mods {
    tapping-term-ms = <175>;      // Hold threshold
    quick-tap-ms = <125>;         // Quick tap threshold
    require-prior-idle-ms = <150>; // Prevent false triggers
    flavor = "balanced";          // Timing behavior
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

**Note**: This documentation is for ZMK-v2 firmware specifically designed for the Descipline V2 keyboard with Nice!Nano v2 or nrf promicro controller. For other keyboards or controllers, configuration details may differ.
