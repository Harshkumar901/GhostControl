# 👻 GhostControl

> **A secure Windows + Android workstation control system for remote input, gesture control, media, gaming, screen linking, and intelligent automation.**

![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Android-0d1117?style=flat-square)
![Android](https://img.shields.io/badge/Android-Flutter-0d1117?style=flat-square&logo=flutter)
![Windows](https://img.shields.io/badge/Windows-PyQt6-0d1117?style=flat-square&logo=windows)
![Security](https://img.shields.io/badge/Security-Ed25519-0d1117?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active%20Development-0d1117?style=flat-square)

---

## Overview

**GhostControl** is a cross-platform workstation control system designed to turn an Android device into a powerful remote interface for a Windows PC.

The system combines:

- A native **Windows workstation application**
- A **Flutter-based Android controller**
- Computer-vision gesture recognition
- Remote mouse and keyboard input
- Media control
- Gaming controls
- Screen Link
- Quick Launch
- Trusted-device security
- Capability-based authorization

GhostControl is being developed as a **real product**, with emphasis on security, modularity, responsive interaction, and practical workstation use.

---

## ✨ Core Features

### 🖥️ Windows Workstation

The Windows application acts as the authoritative workstation host and control center.

- Native PyQt6 control center
- Workstation status and diagnostics
- Gesture-based computer control
- Remote mouse control
- Remote keyboard input
- Windows media control
- Gaming control
- Screen Link
- Quick Launch
- Power controls
- Trusted-device management
- Security and session management

---

### 📱 Android Controller

The Android application provides the remote control interface.

- Flutter-based UI
- Mousepad / trackpad
- Full virtual keyboard
- Gaming controller
- Media center
- Screen Link interface
- Quick Launch Ghost Orb
- Customizable controls
- Dark Cyber theme
- Metallic Light theme
- Responsive portrait and landscape layouts
- Haptic interaction feedback

---

## ✋ Gesture Control

GhostControl uses computer vision to recognize hand gestures through the Windows workstation camera.

### Gesture mappings

| Gesture | Action |
|---|---|
| Two-finger swipe right | Next tab |
| Two-finger swipe left | Previous tab |
| Pinch outward | Zoom in |
| Pinch inward | Zoom out |
| Open palm hold | Play / Pause |
| Palm downward swipe | Lock workstation |

The gesture pipeline is designed around:

- Hand landmark detection
- Landmark normalization
- Finger-state analysis
- Gesture detection
- Confidence thresholds
- Temporal smoothing
- Activation zones
- State-machine processing
- Debouncing
- Cooldown protection
- Action mapping

### Gesture Pipeline

```text
Camera
  ↓
Hand Landmark Detection
  ↓
Landmark Normalization
  ↓
Gesture Detection
  ↓
Confidence / Smoothing
  ↓
State Machine
  ↓
Action Mapping
  ↓
Security Authorization
  ↓
Windows Action
```

---

## 🎮 Gaming

GhostControl provides a dedicated landscape gaming controller.

### Gaming profiles

- FPS
- Racing
- Action
- Emulator
- Custom

### Controls

- Virtual sticks
- Configurable buttons
- Gyroscope input
- Adjustable sensitivity
- Haptic feedback
- Custom button positioning
- Button resizing
- Show / hide controls
- Persistent per-profile mappings

The gaming controller is designed so that control configuration is associated with individual profiles rather than being globally fixed.

---

## 🖥️ Screen Link

**Screen Link** provides a framework for authenticated screen communication between Windows and Android.

The architecture supports three operating modes:

```text
Laptop → Phone
Phone  → Laptop
Bidirectional
```

Each direction can operate independently with its own streaming and control state.

### Control separation

GhostControl separates:

**View Only**

```text
Screen Stream
     ↓
Display
```

from:

**Remote Control**

```text
Screen Stream
     ↓
Authenticated Session
     ↓
Security Authorization
     ↓
Remote Input
```

Displaying a screen does not automatically grant input-control permissions.

Screen control is treated as a separate capability.

---

## ⚡ Quick Launch

GhostControl includes a floating **Ghost Orb** for quickly accessing configured workstation actions and applications.

### Ghost Orb

- Floating launcher
- Radial menu
- Customizable slots
- GhostControl modules
- Installed Windows applications
- Drag-to-position
- Persistent position
- Configurable diameter
- Configurable opacity
- Automatic landscape hiding
- Responsive edge-aware radial positioning

The launcher is designed around an allowlisted Windows application registry.

The Android controller sends an application identifier rather than an arbitrary executable path.

```text
Android
   ↓
Application ID
   ↓
Windows Application Registry
   ↓
Security Authorization
   ↓
Registered Application
```

This prevents the Android client from directly requesting arbitrary executable paths.

---

## 🔐 Security Architecture

Security is a foundational part of GhostControl.

The architecture is designed around **device identity, authenticated sessions, capabilities, and centralized authorization**.

### Security components

- Ed25519 device authentication
- Trusted-device identities
- Challenge-response authentication
- Fresh nonces
- Replay protection
- Session expiration
- Capability-based authorization
- Rate limiting
- Security auditing
- Trusted-device management
- Centralized Security Gateway

Privileged workstation actions are intended to pass through the Security Gateway before reaching the operating-system action layer.

### Security flow

```text
Android Device
      ↓
Device Identity
      ↓
Authentication
      ↓
Authenticated Session
      ↓
Capability Check
      ↓
Security Gateway
      ↓
Action Mapper
      ↓
Windows Action
```

### Security principles

GhostControl is designed to avoid:

- Arbitrary executable paths
- `shell=True`
- Command-shell execution
- PowerShell execution
- `eval()` / `exec()`
- Password transmission
- Unauthenticated privileged commands
- Direct OS access from remote clients

The production implementation and security-sensitive source code are intentionally kept private.

---

## 🧩 Architecture

At a high level:

```text
                    ┌─────────────────────────┐
                    │        Android          │
                    │    Flutter Controller   │
                    └────────────┬────────────┘
                                 │
                                 │
                         Authenticated
                         Communication
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │    Security Gateway     │
                    │                         │
                    │ Authentication          │
                    │ Authorization           │
                    │ Sessions                │
                    │ Replay Protection       │
                    │ Rate Limiting           │
                    │ Audit                   │
                    └────────────┬────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │      Action Mapper      │
                    └────────────┬────────────┘
                                 │
              ┌──────────────────┼──────────────────┐
              ▼                  ▼                  ▼
       Input Control       Media Control      System Control
              │                  │                  │
              └──────────────────┼──────────────────┘
                                 │
                                 ▼
                    ┌─────────────────────────┐
                    │      Windows Host       │
                    │                         │
                    │ Input / Media / Apps    │
                    │ Gaming / Power          │
                    │ Gesture Control         │
                    └─────────────────────────┘
```

---

## 🛠️ Technology Stack

### Windows

| Technology | Purpose |
|---|---|
| Python | Core workstation application |
| PyQt6 | Desktop UI |
| OpenCV | Camera processing |
| MediaPipe Tasks | Hand landmark detection |
| PyAutoGUI | Input automation |
| pycaw | Windows audio control |
| pynput | Input handling |
| WebSockets | Android ↔ Windows communication |
| Cryptography | Security primitives |
| QR generation | Device pairing |
| pytest | Automated testing |

### Android

| Technology | Purpose |
|---|---|
| Flutter | Application framework |
| Dart | Application language |
| WebSockets | Remote communication |
| Secure platform storage | Device identity protection |
| Mobile Scanner | QR pairing |
| MediaProjection | Android screen capture |
| Haptic feedback | Interaction feedback |

---

## 🎨 Design System

GhostControl uses a futuristic **cyber-workstation** visual language.

### Dark Cyber

- Deep navy / black surfaces
- Glass panels
- Electric cyan / blue accents
- Green active states
- Purple gaming states
- Magenta media states
- Orange warnings
- Red errors

### Metallic Light

- Pearl and metallic surfaces
- Light glass materials
- Subtle reflections
- Technical borders
- Controlled accent lighting

### Interaction

The interface uses restrained motion rather than excessive animation.

Examples include:

- Keyboard press feedback
- Haptic feedback
- Ghost Orb breathing animation
- Radial menu transitions
- Color-wheel expansion
- Navigation transitions
- Responsive landscape transitions

Semantic status colors remain independent from the customizable GhostControl accent.

---

## 📚 Documentation

Detailed public documentation will be organized under [`docs/`](docs/).

Planned documentation:

| Document | Description |
|---|---|
| `architecture.md` | System architecture |
| `security-architecture.md` | Security model and trust boundaries |
| `gesture-system.md` | Gesture recognition pipeline |
| `android-controller.md` | Android controller architecture |
| `screen-link.md` | Screen Link architecture |
| `quick-launch.md` | Ghost Orb and application launching |
| `roadmap.md` | Development roadmap |

---

## 🔒 Public Repository Policy

This repository is the **public showcase and documentation repository** for GhostControl.

The production implementation is maintained separately.

### Public repository may contain

- Architecture documentation
- Product screenshots
- UI demonstrations
- Technical explanations
- Public-safe examples
- Design documentation
- Development notes
- Roadmap information

### Never commit

- Private keys
- Ed25519 private keys
- Android signing keystores
- Play Store credentials
- Firebase service-account credentials
- API secrets
- Production tokens
- Passwords
- Internal authentication material
- Proprietary production source
- Security-sensitive deployment components

The public repository intentionally does not contain the complete production implementation.

---

## 🚧 Development Status

GhostControl is under active development.

The project is being developed as a real Windows + Android product rather than a demonstration-only college project.

Feature availability and verification status may change during development.

Where appropriate, documentation distinguishes between:

- **Implemented**
- **Automated Tested**
- **Physically Verified**
- **Planned**
- **Not Yet Verified**

Documentation should not be interpreted as proof that an individual feature is production-ready unless explicitly verified.

---
## 📸 Screenshots

> The screenshots below show the current GhostControl interface and design direction.
> Some modules are still under active development and functionality may change.

### Home

![GhostControl Home](screenshots/home.png)

### Input — Mousepad

![GhostControl Mousepad](screenshots/mousepad.png)

### Input — Keyboard

![GhostControl Keyboard](screenshots/keyboard.png)

### Settings

![GhostControl Settings](screenshots/settings.png)

### App Appearance

![GhostControl Appearance](screenshots/appearance.png)

### Security & Access

![GhostControl Security](screenshots/security.png)

### Screen Link

![GhostControl Screen Link](screenshots/screen-link.png)

### Media Center

![GhostControl Media](screenshots/media.png)

## 🗺️ Roadmap

### Core Platform

- [x] Windows workstation architecture
- [x] Android controller architecture
- [x] Remote input architecture
- [x] Gesture recognition pipeline
- [x] Media control architecture
- [x] Quick Launch architecture
- [x] Security Gateway architecture
- [x] Screen Link architecture

### Security

- [x] Device identity architecture
- [x] Capability-based authorization architecture
- [x] Replay protection architecture
- [ ] Security hardening
- [ ] Transport encryption audit
- [ ] Trusted-device storage hardening
- [ ] Full security review

### Product

- [ ] Extended gaming profiles
- [ ] Performance optimization
- [ ] Expanded device management
- [ ] UI refinement
- [ ] Release preparation
- [ ] Google Play release

---

## ⚠️ Security Disclosure

If you discover a potential security vulnerability in GhostControl, please avoid publicly posting sensitive exploit details.

Security-related reports should be handled privately.

See [`SECURITY.md`](SECURITY.md) for the responsible disclosure policy.

---

## 👨‍💻 Author

**Harsh Punia**

GhostControl is an independently developed software project focused on building a secure, modular bridge between Android devices and Windows workstations.

---

## 👻 GhostControl

> **Control your workstation. Your way.**
