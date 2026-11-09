# PhantomMouse

**Hardware-assisted mouse control system with real-time computer vision, object detection and Arduino integration.**

## Overview

PhantomMouse is an experimental mouse control system that combines physical mouse input, computer vision and Arduino-based hardware integration.

The system uses a secondary computer to analyze a video feed from the main computer. Based on detected objects, colors or positions, it can calculate mouse movement commands and transmit them to an Arduino Leonardo.

The Arduino combines these calculated movements with the physical mouse input and forwards the resulting input to the main computer.

## Project Goals

- Real-time video capture and image processing.
- Object and color detection using OpenCV.
- Physical mouse input passthrough.
- Hardware-assisted mouse movement.
- Low-latency serial communication.
- Modular Python software architecture.
- Expandable system with additional hardware.

## Hardware Architecture

### Main PC
- AMD Ryzen 7 5700X
- NVIDIA RTX 2060 (6 GB VRAM)
- Gaming monitor (165 Hz)
- Arduino Leonardo R3 connected as a USB HID device.

### Secondary PC
- Intel Core i3-12100F
- NVIDIA GTX 750 Ti
- Video capture card
- Python and OpenCV processing environment.

### Microcontroller
- Arduino Leonardo R3 (ATmega32u4)
- USB Host Shield 2.0
- CP2102 USB-to-TTL serial adapter

### Video Capture
- XIIXMASK USB 3.0 HDMI capture card (planned)
- HDMI passthrough to the main monitor.
- Video stream analyzed by the secondary PC.

**Note:** Hardware compatibility, especially 165 Hz passthrough and USB Host Shield support, must be verified before final implementation.

## Software Architecture

Planned software modules:

| Module | Responsibility |
|---|---|
| `main.py` | Main application and coordination |
| `capture.py` | Video capture |
| `detection.py` | Object and color detection |
| `tracking.py` | Object tracking and position calculation |
| `serial_comm.py` | Communication with Arduino |
| `config.py` | Configuration and settings |

## Technology Stack

- Python
- OpenCV
- NumPy
- PySerial
- Arduino C++
- USB Host Shield Library

## Development Roadmap

### Phase 1 – Foundation
- Set up repository and development environment.
- Establish Python project structure.
- Test video capture.
- Verify serial communication.

### Phase 2 – Computer Vision
- Implement color detection.
- Implement object detection.
- Add tracking and position calculation.
- Optimize processing performance.

### Phase 3 – Arduino Integration
- Establish reliable mouse passthrough.
- Implement serial command protocol.
- Combine physical and calculated mouse movements.
- Test HID output.

### Phase 4 – Optimization
- Reduce latency.
- Improve tracking stability.
- Add configurable sensitivity and detection parameters.
- Build a simple control interface.

### Phase 5 – Expansion
- Modular detection algorithms.
- Advanced tracking.
- Improved user interface.
- Additional hardware integrations.

## Development Principles

- Keep the code modular and maintainable.
- Do not assume hardware compatibility without testing.
- Avoid unnecessary dependencies.
- Document important changes.
- Test each module independently.
- Never commit experimental changes directly to `main`.

## Repository Structure

```text
phantom-mouse/
├── README.md
├── PROJECT_RULES.md
├── CHANGELOG.md
├── .gitignore
├── requirements.txt
├── firmware/
│   └── phantom_mouse/
├── src/
│   └── phantom_mouse/
└── tests/
```

## Safety and Intended Use

PhantomMouse is intended for authorized automation, accessibility experiments, computer vision research and testing on systems controlled by the user.

It is not designed for anti-cheat evasion, stealth automation or unauthorized manipulation of third-party systems.

## Project Status

<badge>In development</badge>

Currently in the planning and hardware verification stage.

No hardware compatibility should be considered confirmed until it has been tested.
