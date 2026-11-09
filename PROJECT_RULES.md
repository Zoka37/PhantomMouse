# PROJECT RULES – AI Mouse Control

**Project:** AI Mouse Control  
**Status:** Development / Prototype  
**Language:** German for communication, English for code, comments and variable names.

---

## 1. Project Goal

Develop a hardware-assisted mouse control system using two computers, an Arduino Leonardo R3, a USB Host Shield and an HDMI capture card.

The system should combine physical mouse input with additional calculated mouse movements.

The second PC analyzes the captured screen image, detects configured colors or objects, calculates their screen positions and sends movement commands to the Arduino.

The project should be modular, reliable, responsive and easy to expand.

## 2. Hardware Configuration

### Main PC – Development and AI Coding

- CPU: AMD Ryzen 7 5700X
- GPU: NVIDIA RTX 2060
- VRAM: 6 GB
- Purpose:
  - Running Bionic
  - Running Qwen2.5-Coder-7B-Instruct-Heretic locally
  - Developing and managing the project
  - Testing and debugging code

The language model is a development tool. It is not intended to run the screen recognition system.

### Second PC – Image Processing

- CPU: Intel Core i3-12100F
- GPU: NVIDIA GTX 750 Ti
- RAM: Initially 8 GB DDR4, possible upgrade to 16 GB
- Purpose:
  - Receiving captured video
  - Image processing
  - Color detection
  - Object detection
  - Position calculations
  - Sending commands to the Arduino

Optimize the software for this hardware. Avoid unnecessarily demanding AI models.

### Arduino

- Arduino Leonardo R3
- USB Host Shield 2.0
- CP2102 USB-to-TTL serial adapter

Responsibilities:

- Reading the physical USB mouse
- Receiving commands from the second PC
- Combining physical and calculated mouse movements
- Sending the resulting mouse input to the main PC

Verify the USB Host Shield wiring, SPI connections and library compatibility before implementing the mouse input.

### Capture Card

Currently considered:

- XIIXMASK USB 3.0 Capture Card
- HDMI input
- HDMI passthrough output
- USB 3.0 connection to the second PC
- Advertised capture: 1080p60

Important:
- 1080p165 passthrough has not yet been verified.
- Do not assume that the capture card supports 165 Hz.
- Preserve the main monitor's refresh rate whenever possible.
- Check compatibility before finalizing the video connection.

## 3. System Architecture

The intended data flow:

1. The main PC generates the video signal.
2. The capture card receives the video signal.
3. The second PC receives the captured image.
4. Python and OpenCV analyze the image.
5. The software detects configured colors or objects.
6. The software calculates their positions.
7. The second PC sends movement commands through the CP2102.
8. The Arduino receives the commands through its hardware UART.
9. The Arduino combines physical mouse input and calculated movement.
10. The Arduino outputs the combined HID mouse input to the main PC.

The physical mouse must remain usable while the additional movement system is active.

## 4. Software Architecture

Preferred programming languages:

- Python for image processing and communication.
- C++ / Arduino for the Leonardo firmware.

Preferred Python libraries:

- OpenCV
- NumPy
- PySerial

Possible modules:

### capture.py
- Capture card initialization
- Video frame acquisition
- Frame validation
- Resolution management

### detection.py
- Color detection
- Object detection
- Position extraction
- Configurable detection parameters

### tracking.py
- Object position tracking
- Movement estimation
- Detection stability

### serial_comm.py
- Serial connection
- Command transmission
- Error handling
- Connection monitoring

### main.py
- Main application
- Module coordination
- Configuration loading
- Logging

Arduino modules should be separated logically into:

- Physical mouse input
- Serial command processing
- Mouse movement combination
- HID output

## 5. Performance Requirements

The software should prioritize:

1. Low latency
2. Stable frame acquisition
3. Efficient CPU and GPU usage
4. Low memory consumption
5. Reliable serial communication
6. Stable mouse input

Initial target:

- Input resolution: 1080p
- Capture rate: Up to 60 FPS
- Image processing: As fast as practical
- Configurable detection sensitivity
- Configurable color ranges
- Adjustable movement parameters

Do not sacrifice system stability for unnecessary performance optimizations.

## 6. Development Rules for the AI Coding Agent

These rules are mandatory.

### Before changing code

1. Inspect the existing project structure.
2. Read relevant source files.
3. Understand existing functionality.
4. Identify dependencies and hardware requirements.
5. Explain the proposed changes before major modifications.

### When modifying code

- Preserve working functionality.
- Avoid unnecessary rewrites.
- Keep modules separated.
- Use descriptive English variable and function names.
- Handle errors properly.
- Avoid unnecessary dependencies.
- Document important hardware-specific behavior.
- Do not invent hardware capabilities.
- Never silently remove existing functionality.

### Testing

After each meaningful change:

1. Check for syntax errors.
2. Run available tests.
3. Verify module compatibility.
4. Explain what was changed.
5. List remaining problems or untested hardware behavior.

Never claim hardware functionality has been verified if it has only been simulated.

## 7. Git and Version Control

The project uses a private GitHub repository.

Rules:

- Never work directly on the main branch.
- Use a separate development branch or feature branches.
- Create commits before major modifications.
- Keep commits small and descriptive.
- Never overwrite working versions without a backup.
- Keep experimental code separate from stable code.

## 8. Configuration

Hardware-dependent values should be configurable rather than hardcoded.

Examples:

- Serial port
- Serial baud rate
- Capture resolution
- Capture frame rate
- Detection color ranges
- Detection thresholds
- Movement sensitivity
- Tracking parameters

Use a central configuration file wherever practical.

## 9. Security and Responsible Use

The system is intended for authorized automation, accessibility, computer vision experiments and testing on systems controlled by the user.

Do not implement anti-cheat evasion, stealth mechanisms or unauthorized manipulation of third-party software.

Do not store passwords, API keys or other secrets in the repository.

## 10. Long-Term Development Goal

The final system should provide:

- Reliable physical mouse passthrough
- Configurable color recognition
- Configurable object recognition
- Object position tracking
- Low-latency processing
- Stable communication between both PCs
- Modular and maintainable source code
- Expandability for future hardware and software improvements

**Most important instruction: Build a working prototype first. Improve it incrementally. Do not overcomplicate the initial implementation.**
