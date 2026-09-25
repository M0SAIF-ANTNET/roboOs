# RoboOS
<p align="center">
  <img src="https://github.com/user-attachments/assets/00ee3db5-e2a3-4a11-868f-9f71f39c7630" alt="logo_roboos_main_no_bg" width="300" />
</p>

> **A robotics-first, terminal-first Linux operating system for robotics development, AI, computer vision, embedded systems, simulation, and hardware integration.**

RoboOS is a lightweight, developer-oriented Linux operating system designed specifically around the needs of robotics engineers, researchers, and developers.

It is built on **Ubuntu 24.04 LTS** while providing a dedicated robotics-oriented environment, system tooling, hardware management, development workflows, and a unified RoboOS command interface.

The goal is not to create another Ubuntu distribution with ROS preinstalled.

RoboOS is designed as a **robotics development platform** where operating-system tools, hardware interfaces, development environments, robotics workspaces, and system configuration are organized around robotics workflows.

---

## 1. Vision

Robotics development often requires working across many layers of the computing stack:

```text
Hardware
   ↓
Linux Kernel
   ↓
Devices / Drivers / Services
   ↓
Development Tools
   ↓
ROS / Robotics Middleware
   ↓
Computer Vision / AI
   ↓
Robotics Applications
```

RoboOS aims to provide a coherent environment across these layers.

Instead of forcing developers to manually assemble a robotics workstation from a generic Linux installation, RoboOS provides a dedicated foundation for:

* Robotics development
* Embedded systems
* Computer vision
* Artificial intelligence
* Sensors
* Cameras
* Serial communication
* CAN bus
* USB devices
* GPU computing
* ROS development
* Simulation
* Hardware integration
* Robotics workspaces

---

# 2. Core Philosophy

RoboOS follows several principles.

## Robotics-first

The operating system is organized around robotics development rather than general desktop usage.

## Terminal-first

The terminal is a first-class interface.
<p align="center">
  <img src="https://github.com/user-attachments/assets/ba2e1d33-3a43-4b07-b9f6-468a2bc43311" alt="image" width="600" />
</p>

<br />
The graphical interface is optional and exists to make system management easier when a GUI provides a meaningful advantage.

## Hardware-aware

RoboOS treats physical hardware as a central part of the operating system experience.

The system provides dedicated interfaces for:

* USB
* PCI devices
* Wi-Fi
* Bluetooth
* Cameras
* Serial devices
* CAN
* Audio
* Displays
* Storage
* GPU information

## Native Linux underneath

RoboOS does not attempt to replace Linux's existing hardware and system infrastructure.

Instead, it provides a higher-level interface over established Linux technologies.

```text
RoboOS Interface
       ↓
RoboOS Backend
       ↓
Linux APIs / Services / Utilities
       ↓
Kernel / Drivers
       ↓
Hardware
```

This keeps the system compatible with the existing Linux ecosystem.

## Developer-oriented

RoboOS includes a development foundation suitable for robotics software, AI, computer vision, embedded systems, and systems programming.

---

# 3. Base System

RoboOS is based on:

| Component              | Technology             |
| ---------------------- | ---------------------- |
| Base OS                | Ubuntu 24.04 LTS       |
| Codename               | Noble                  |
| Architecture           | x86_64 / amd64         |
| Init System            | systemd                |
| Kernel                 | Linux                  |
| Package Management     | APT / dpkg             |
| Desktop Environment    | XFCE 4.18              |
| Display Server         | Xorg                   |
| Display Manager        | None                   |
| GUI Startup            | `startx`               |
| Audio                  | PipeWire + WirePlumber |
| Networking             | NetworkManager         |
| Bluetooth              | BlueZ                  |
| Storage Management     | UDisks                 |
| Virtualization Testing | QEMU/KVM               |
| Firmware Interface     | UEFI / OVMF            |

RoboOS intentionally retains Ubuntu's underlying package ecosystem and hardware compatibility.

---

# 4. System Architecture

The system is divided into several conceptual layers.

```text
┌─────────────────────────────────────────────┐
│              RoboOS Applications            │
│                                             │
│ Settings │ Files │ Browser │ Workspace      │
└──────────────────────┬──────────────────────┘
                       │
┌──────────────────────▼──────────────────────┐
│              RoboOS Interface               │
│                                             │
│             robo CLI                        │
│             GTK Settings                    │
└──────────────────────┬──────────────────────┘
                       │
┌──────────────────────▼──────────────────────┐
│              RoboOS Backend                 │
│                                             │
│ System │ Network │ Bluetooth │ Audio        │
│ Power  │ Display │ Storage │ Hardware       │
└──────────────────────┬──────────────────────┘
                       │
┌──────────────────────▼──────────────────────┐
│          Linux Services / APIs              │
│                                             │
│ NetworkManager │ BlueZ │ UDisks │ PipeWire  │
│ systemd │ Xorg │ xrandr │ sysfs │ nmcli     │
└──────────────────────┬──────────────────────┘
                       │
┌──────────────────────▼──────────────────────┐
│              Linux Kernel                   │
└──────────────────────┬──────────────────────┘
                       │
┌──────────────────────▼──────────────────────┐
│               Hardware                     │
└─────────────────────────────────────────────┘
```

The architecture deliberately avoids unnecessary reinvention.

For example, RoboOS does not implement its own networking stack.

Instead:

```text
RoboOS Network UI
        ↓
RoboOS network.py
        ↓
NetworkManager / nmcli
        ↓
Linux networking
```

The same principle is applied throughout the system.

---

# 5. RoboOS Command Interface

RoboOS provides a unified command-line interface through:

```bash
robo
```

The CLI is intended to become the primary system-management interface for robotics developers.

Current command structure:

```text
robo info
robo doctor
robo devices
robo settings
robo workspace
```

The architecture is designed to support additional robotics-oriented commands:

```text
robo init
robo network
robo camera
robo serial
robo can
robo ros
```

## `robo info`

Displays RoboOS identity and system information.

Example:

```bash
robo info
```

Information includes:

* RoboOS name
* Version
* Base system
* Codename
* Kernel
* Architecture

---

## `robo doctor`

Performs a basic RoboOS environment health check.

```bash
robo doctor
```

It checks important development and system components such as:

* NetworkManager
* USB tools
* PCI tools
* Python
* CMake
* Git
* GDB

The command is intended to become a more comprehensive robotics environment diagnostic system.

---

## `robo devices`

Provides an overview of connected hardware.

```bash
robo devices
```

The interface covers:

* USB
* PCI
* Network interfaces

The architecture also supports dedicated robotics hardware discovery for:

* Cameras
* Serial devices
* CAN devices
* Bluetooth devices
* Storage
* GPUs

---

# 6. RoboOS Settings

RoboOS includes a custom GTK4 settings application.

Launch it using:

```bash
robo settings
```

or through the RoboOS desktop environment.

The application provides a centralized interface for system and robotics-related configuration.

## Settings sections

### Overview

Provides a general system overview.

### Display

Manages:

* Displays
* Outputs
* Resolution
* Display modes
* Brightness

Uses Linux/X11 interfaces such as:

* `xrandr`
* sysfs

### Network

Provides Wi-Fi and network management.

Capabilities include:

* Wi-Fi status
* Enable/disable Wi-Fi
* Network discovery
* Signal information
* Security information
* Wi-Fi connection
* Password handling
* Network disconnection
* Network device information

The underlying networking system is NetworkManager.

### Power

Provides power-management controls.

Supported profiles include:

```text
Performance
Balanced
Power Saver
```

Battery information includes:

* Battery availability
* Charge level
* Charging status
* Time information

The underlying power-management system uses `power-profiles-daemon`.

### Storage

Provides storage information and integration with the Linux storage stack.

RoboOS uses:

* UDisks
* Linux filesystems
* Thunar
* GVfs

### CPU & Memory

Provides information about:

* CPU
* Memory
* System resources

### GPU

Provides GPU information through the underlying Linux hardware interfaces.

### USB

Provides information about connected USB devices.

### Bluetooth

Provides Bluetooth management including:

* Bluetooth power
* Device scanning
* Pairing
* Connecting
* Disconnecting
* Removing paired devices
* Paired-device information

The underlying implementation uses:

```text
BlueZ
bluetoothctl
rfkill
```

### Audio

RoboOS uses:

```text
PipeWire
WirePlumber
PulseAudio compatibility
```

The audio interface supports:

* Audio device discovery
* Output selection
* Volume control
* Mute/unmute
* Audio status

### Cameras

Provides camera discovery and robotics-oriented camera information.

### Serial

Provides interfaces for serial-device discovery and future serial-device workflows.

This is particularly relevant for:

* Microcontrollers
* Embedded boards
* Development boards
* Robotics controllers
* Sensors

### CAN

Provides a dedicated area for CAN-bus hardware and robotics communication.

### ROS

Provides a dedicated location for ROS-related information and tooling.

### Workspace

Provides information about the RoboOS robotics development workspace.

### Development

Provides information about the installed development environment.

### Appearance

Controls RoboOS visual configuration.

### Diagnostics

Provides system diagnostics and troubleshooting information.

### About

Provides RoboOS identity and project information.

---

# 7. RoboOS Backend

The GUI is intentionally not responsible for directly implementing low-level system functionality.

Instead, RoboOS uses backend modules.

Important backend components include:

```text
/usr/local/lib/roboos/
```

Examples include:

```text
core.py
system.py
network.py
bluetooth.py
audio.py
display.py
power.py
```

The architecture follows:

```text
GTK Settings
      ↓
system.py
      ↓
specialized backend
      ↓
Linux service / command / API
```

This allows the same functionality to eventually be used by both GUI and CLI interfaces.

---

# 8. Networking Architecture

RoboOS uses NetworkManager as the primary networking infrastructure.

The system supports:

```text
Wi-Fi
Ethernet
Network interfaces
Connection management
```

The RoboOS backend provides an abstraction over NetworkManager.

Example architecture:

```text
RoboOS Settings
      ↓
network.py
      ↓
NetworkManager
      ↓
Linux networking
```

This preserves compatibility with standard Linux networking tools while providing a dedicated RoboOS experience.

---

# 9. Bluetooth Architecture

Bluetooth is provided through BlueZ.

The architecture is:

```text
RoboOS Settings
      ↓
bluetooth.py
      ↓
bluetoothctl / BlueZ
      ↓
Linux Bluetooth subsystem
      ↓
Bluetooth hardware
```

Supported workflows include:

```text
Power
Scan
Pair
Connect
Disconnect
Remove
Device information
```

---

# 10. Audio Architecture

RoboOS uses the modern Linux audio stack:

```text
Applications
     ↓
PipeWire
     ↓
WirePlumber
     ↓
ALSA
     ↓
Audio hardware
```

PulseAudio-compatible interfaces are retained for compatibility.

The system includes utilities such as:

```text
wpctl
pactl
pw-cli
pw-dump
```

This allows both modern PipeWire applications and existing Linux audio software to function.

---

# 11. Display Architecture

RoboOS uses Xorg and XFCE for its current graphical environment.
<img width="1279" height="800" alt="image" src="https://github.com/user-attachments/assets/55ceafde-15e1-49c3-85d3-caa77a5a2f98" />


```text
RoboOS GUI
    ↓
XFCE
    ↓
Xorg
    ↓
GPU driver
    ↓
Display hardware
```

Display management uses:

```text
xrandr
sysfs
```

The design allows future migration toward other display technologies without coupling RoboOS applications directly to a particular implementation.

---

# 12. Desktop Environment

RoboOS uses **XFCE 4.18**.

The desktop is intentionally lightweight and avoids unnecessary desktop components.

The system does not use a traditional graphical display manager.

Instead:

```text
TTY
 ↓
startx
 ↓
XFCE
```

This preserves the terminal-first philosophy while still providing a complete graphical environment when needed.

---

# 13. RoboOS Desktop

The RoboOS desktop includes a custom application menu and panel.

The menu is organized around robotics development.

Main categories include:

```text
Robotics
Development
Hardware
Applications
```

Robotics-oriented applications include:

* RoboOS Settings
* RoboOS Devices
* RoboOS Doctor
* RoboOS Workspace

Development tools include:

* Terminal
* Vim
* htop

Hardware tools include:

* Audio configuration

General applications include:

* RoboOS Files
* RoboOS Browser

---

# 14. RoboOS Files

RoboOS provides a dedicated file-management experience built on existing Linux infrastructure.

Architecture:

```text
RoboOS Files
     ↓
Thunar
     ↓
GVfs
     ↓
UDisks
     ↓
Linux filesystem
```

RoboOS intentionally does not implement a new filesystem or file manager.

Thunar provides:

* File browsing
* Folder management
* Storage access
* Device access
* File operations

RoboOS adds robotics-specific integration.

---

# 15. Robotics Workspace

The default RoboOS robotics workspace is:

```text
~/robot_ws
```

Structure:

```text
robot_ws/
├── src/
├── build/
├── install/
└── log/
```

The structure is compatible with common robotics and ROS development workflows.

A workspace README is automatically provided.

RoboOS also provides:

```bash
robo workspace
```

for workspace-related information.

The graphical environment provides a dedicated RoboOS Workspace launcher.

---

# 16. Thunar Robotics Integration

RoboOS integrates robotics workflows into the file manager.

Custom actions include:

```text
Open Terminal Here
Open RoboOS Workspace
Open Workspace Source
RoboOS Workspace Terminal
```

This allows developers to move directly between:

```text
Files
 ↓
Workspace
 ↓
Terminal
 ↓
Development
```

without requiring a custom file manager.

---

# 17. Web Browser

RoboOS uses **Falkon** as its native lightweight browser.

The browser is integrated through:

```text
/usr/local/bin/robo-browser
```

The RoboOS desktop exposes it through:

```text
RoboOS Browser
```

The decision avoids depending on a Snap-based Firefox installation while keeping a native Debian/Ubuntu package workflow.

---

# 18. Developer Environment

RoboOS provides a core software-development environment suitable for robotics and systems development.

Core tools include:

```text
build-essential
CMake
Git
GDB
Python 3
pip
venv
pkg-config
curl
wget
unzip
Nano
Vim
htop
```

Hardware-development utilities include:

```text
usbutils
pciutils
```

The environment is suitable as a foundation for:

* C/C++
* Python
* Embedded development
* Robotics software
* Computer vision
* AI
* Systems programming
* ROS
* Hardware integration

---

# 19. Hardware Support

RoboOS is designed to retain the broad hardware compatibility of Ubuntu/Linux.

The system supports the Linux hardware ecosystem rather than replacing it.

Important hardware areas include:

```text
CPU
GPU
RAM
USB
PCI
Wi-Fi
Bluetooth
Audio
Camera
Storage
Display
Serial
CAN
```

Useful low-level utilities include:

```bash
lsusb
lspci
nmcli
bluetoothctl
rfkill
udisksctl
wpctl
xrandr
```

The RoboOS layer organizes these capabilities into a robotics-oriented interface.

---

# 20. Robotics Hardware

RoboOS is designed to serve as a host environment for robotics hardware such as:

* Microcontrollers
* Development boards
* Sensors
* Cameras
* LiDAR
* IMUs
* Motor controllers
* USB devices
* Serial devices
* CAN devices
* Embedded computers
* Robotic platforms

The architecture is designed to make these devices visible through both Linux tools and higher-level RoboOS tooling.

---

# 21. ROS Integration

ROS is treated as a major robotics development layer rather than as the operating system itself.

The intended architecture is:

```text
RoboOS
   ↓
Linux
   ↓
ROS
   ↓
Robotics applications
```

RoboOS provides a dedicated ROS area and workspace structure while maintaining compatibility with the normal ROS ecosystem.

Future RoboOS tooling can provide commands such as:

```bash
robo ros
robo ros init
robo ros doctor
robo ros workspace
```

---

# 22. AI and Computer Vision

RoboOS is designed to support AI and computer-vision workloads commonly used in modern robotics.

The base development environment can support:

* Python
* C/C++
* Computer vision frameworks
* Machine-learning frameworks
* GPU acceleration
* Camera pipelines
* Robotics perception

The architecture intentionally does not hard-code a single AI framework.

This allows developers to use ecosystems such as:

```text
OpenCV
PyTorch
TensorFlow
ONNX
CUDA-based tooling
```

when compatible with their hardware.

---

# 23. Embedded Systems

RoboOS is designed to work as a development environment for embedded robotics.

Typical workflow:

```text
RoboOS
   ↓
Compiler / Build System
   ↓
Embedded firmware
   ↓
USB / Serial / Debug interface
   ↓
Microcontroller
   ↓
Sensors / Actuators
```

The system's developer tooling and hardware-management layer are designed to support this workflow.

---

# 24. System Configuration

RoboOS configuration is centralized under:

```text
/etc/roboos/
```

Important configuration files include:

```text
system.conf
gui.conf
```

Example system configuration:

```bash
ROBOOS_NAME="RoboOS"
ROBOOS_VERSION="0.1"
ROBOOS_BASE="Ubuntu 24.04 LTS"
ROBOOS_CODENAME="Noble"
ROBOOS_MODE="terminal-first"
ROBOOS_GUI="optional"
```

GUI configuration defines:

* Theme
* Icons
* Wallpapers
* Desktop environment
* Display server
* Display manager
* Session command

---

# 25. File System Organization

RoboOS uses a structured layout for its own components.

```text
/etc/roboos/
    System configuration

/usr/share/roboos/
    Shared RoboOS assets

/usr/local/lib/roboos/
    RoboOS backend modules

/usr/local/bin/
    RoboOS command-line tools

/opt/roboos/
    Reserved RoboOS application/integration space

/etc/skel/robot_ws/
    Default robotics workspace template
```

This keeps RoboOS components separated from the underlying Ubuntu filesystem.

---

# 26. Branding

RoboOS includes a dedicated visual identity.

Branding assets are stored under:

```text
/usr/share/roboos/branding/
```

The system includes:

```text
logo_roboos_main_no_bg.png
logo_roboos_main.png
logo_roboos_second_no_bg.png
logo_roboos_second.png
```

Separate assets are used for dark and light interfaces.

RoboOS also provides dedicated wallpapers.

---

# 27. Theme

RoboOS uses a dark-oriented visual design.

Current components include:

```text
Greybird-dark
elementary-xfce-dark
```

The interface is designed around:

* Dark UI
* High contrast
* Robotics/developer aesthetics
* Compact information-dense layouts
* Minimal unnecessary decoration

---

# 28. Security and System Services

RoboOS retains important Ubuntu/Linux security and system infrastructure.

Relevant components include:

```text
systemd
UFW
unattended-upgrades
NetworkManager
systemd-resolved
```

The operating system does not remove core Linux services simply for size reduction when doing so would reduce hardware or system compatibility.

---

# 29. Design Decision: Lightweight vs Compatibility

RoboOS does not attempt to win by having the smallest possible ISO.

The priority is:

```text
Functionality
     ↓
Compatibility
     ↓
Developer experience
     ↓
Robotics integration
     ↓
Efficiency
```

Lightweight components are preferred when they provide equivalent or better functionality.

However, critical Linux infrastructure is retained when removing it would compromise:

* Hardware support
* Networking
* Graphics
* Audio
* Storage
* Device management
* Developer workflows

---

# 30. Testing Environment

RoboOS images are tested using QEMU/KVM.

Typical test environment:

```text
QEMU
KVM
Q35 machine
UEFI / OVMF
4 CPU cores
4 GB RAM
32 GB qcow2 disk
VirtIO storage
VirtIO networking
```

Example VM storage:

```text
~/roboOs/vm/
```

Example files:

```text
roboos-buildN.qcow2
roboos-buildN_VARS.fd
```

This allows separate build generations to be tested without modifying the host environment.

---

# 31. Build Workflow

The operating system is assembled using **Cubic** on an Ubuntu-based ISO.

General workflow:

```text
Ubuntu Server ISO
       ↓
Cubic
       ↓
Base system customization
       ↓
RoboOS packages
       ↓
RoboOS backend
       ↓
RoboOS CLI
       ↓
RoboOS Settings
       ↓
Desktop integration
       ↓
Branding
       ↓
ISO generation
       ↓
QEMU/KVM
       ↓
System testing
```

The original Ubuntu ISO is preserved separately from generated RoboOS images.

---

# 32. Development Workflow

A typical RoboOS development session can look like:

```bash
robo info
robo doctor
robo devices
robo workspace
```

Then:

```bash
cd ~/robot_ws
```

Development can proceed using:

```text
C/C++
Python
CMake
Git
GDB
ROS
OpenCV
AI/ML frameworks
Embedded toolchains
```

Hardware can be inspected using RoboOS or standard Linux utilities.

---

# 33. Design Goals

RoboOS is designed to provide:

### 1. A robotics-native developer environment

Robotics tools should feel like part of the operating system rather than manually installed additions.

### 2. A unified interface

The same RoboOS backend should power:

```text
CLI
GUI
Future APIs
Future automation
```

### 3. Hardware visibility

Robotics hardware should be easy to discover and diagnose.

### 4. Linux compatibility

Existing Linux software should continue to work.

### 5. Developer freedom

Developers should still be able to use normal Linux commands and tools.

### 6. Research compatibility

The system should be suitable for academic robotics, AI, and computer-vision research.

### 7. Future extensibility

The architecture should support future robotics-specific services without requiring a complete redesign.

---

# 34. Future Development

RoboOS is designed to evolve beyond the current foundation.

Potential future components include:

```text
robo init
robo network
robo camera
robo serial
robo can
robo ros
robo sensor
robo gpu
robo simulation
```

Additional planned areas include:

* Automatic robotics environment setup
* ROS environment management
* Camera diagnostics
* Sensor diagnostics
* Serial-device tools
* CAN diagnostics
* GPU diagnostics
* Robotics workspace management
* Simulation environment management
* Embedded development workflows
* Hardware health checks
* Robotics development profiles
* Containerized robotics environments
* Reproducible robotics development environments

---

# 35. Long-Term Architecture

The long-term RoboOS architecture is intended to evolve toward:

```text
                    RoboOS
                       │
          ┌────────────┴────────────┐
          │                         │
         CLI                       GUI
          │                         │
          └────────────┬────────────┘
                       │
                RoboOS Backend
                       │
        ┌──────────────┼──────────────┐
        │              │              │
      System        Hardware       Robotics
        │              │              │
     Linux APIs     Devices       ROS / Tools
        │              │              │
        └──────────────┼──────────────┘
                       │
                    Linux
                       │
                    Hardware
```

The objective is to make RoboOS a coherent platform rather than a collection of unrelated utilities.

---

# 36. Project Status

RoboOS currently provides a complete foundational robotics-oriented Linux environment including:

* Ubuntu 24.04 LTS base
* RoboOS identity and configuration
* Custom branding
* XFCE desktop
* Xorg
* Terminal-first startup
* RoboOS CLI
* RoboOS Settings
* Hardware information
* Network management
* Wi-Fi management
* Bluetooth management
* Audio management
* Power management
* Display management
* Storage integration
* USB and PCI inspection
* RoboOS Files
* Robotics workspace
* Custom application menu
* Custom XFCE panel
* Native lightweight browser
* Developer toolchain
* Robotics-oriented directory structure
* QEMU/KVM testing workflow

The architecture is designed to continue expanding into deeper robotics functionality without changing the underlying Linux foundation.

---

# 37. Philosophy

RoboOS is based on a simple idea:

> **Robotics developers should not have to fight their operating system before they can start building robots.**

The operating system should make the relationship between:

```text
Developer
     ↓
Software
     ↓
Robotics Middleware
     ↓
Hardware
```

clear, accessible, and manageable.

RoboOS aims to provide that foundation while preserving the power and flexibility of Linux.

---

# 38. Project Identity

**Project:** RoboOS

**Base:** Ubuntu 24.04 LTS

**Architecture:** amd64 / x86_64

**Desktop:** XFCE

**Display:** Xorg

**Audio:** PipeWire / WirePlumber

**Networking:** NetworkManager

**Bluetooth:** BlueZ

**Storage:** UDisks / GVfs

**Primary interface:** `robo`

**Default workspace:** `~/robot_ws`

**Development model:** Terminal-first, GUI-optional

**Target users:** Robotics developers, researchers, students, embedded developers, AI/CV engineers

---

## License

RoboOS is an independent project built on top of the Ubuntu/Linux ecosystem.

Individual components retain their respective upstream licenses.

RoboOS-specific code, configuration, artwork, and tooling should be licensed separately according to the project's chosen open-source license.

---

## Status

**RoboOS — Robotics-first Linux development environment**

Built around:

**Linux × Robotics × AI × Computer Vision × Hardware**

