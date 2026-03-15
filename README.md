 # 🤖 R2-D2 Style Arduino Robot

> A Bluetooth-controlled obstacle-avoiding robot with R2-D2 personality and sounds!

[![Arduino](https://img.shields.io/badge/Arduino-Uno-00979D?logo=arduino)](https://www.arduino.cc/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Arduino-lightgrey)]()

## 📖 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Demo](#demo)
- [Hardware Requirements](#hardware-requirements)
- [Wiring Diagram](#wiring-diagram)
- [Installation](#installation)
- [Usage](#usage)
- [R2-D2 Personality](#r2d2-personality)
- [Commands](#commands)
- [Modes](#modes)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## 🎯 Overview

This project transforms a simple Arduino robot into a **Star Wars R2-D2-style droid** with personality! The robot features autonomous obstacle avoidance, line following capabilities, and authentic R2-D2 beeps and movements. Control it wirelessly via Bluetooth or through the Serial Monitor.

### What Makes This Special?

- **🎵 R2-D2 Sounds**: Happy beeps, worried boops, excited chirps, and whistles
- **🎭 Character Movements**: Head shakes, nods, and cautious scanning
- **🧠 Smart Navigation**: Autonomous obstacle avoidance with servo head scanning
- **📱 Wireless Control**: Bluetooth connectivity for remote operation
- **👁️ Line Following**: Dual IR sensors for tracking lines
- **🔊 Audio Feedback**: Real-time beeps that match R2-D2's emotions

---

## ✨ Features

### Core Functionality
- ✅ **Bluetooth Control** - Control from smartphone (HC-05 module)
- ✅ **USB Serial Control** - Control via Arduino IDE Serial Monitor
- ✅ **Obstacle Avoidance** - Autonomous navigation with ultrasonic sensor
- ✅ **Line Following** - Follow black lines using dual IR sensors
- ✅ **Servo Head** - 180° scanning for obstacle detection
- ✅ **Audio Feedback** - R2-D2 style beeps and boops via buzzer

### R2-D2 Personality Features
- 🎵 **Happy Beeps** - High-low-high "beep-boop-beep!" when path is clear
- 😟 **Worried Beeps** - Fast low "boop-boop-boop" when obstacles detected
- 🎉 **Excited Beeps** - Rising tones when starting auto mode
- 🎶 **Whistles** - Long melodic beeps on command
- 🤔 **Confused Beeps** - Random tones when both paths blocked
- 👋 **Head Shake** - Servo oscillates when worried or excited
- 👍 **Head Nod** - Servo nods when acknowledging commands

---

## 🎬 Demo

### Robot in Action

```
R2-D2 Powers On:
  🎵 *Excited beeps*
  🤖 *Head shake*
  🎶 *Happy whistle*
  "Beep-boop! R2-D2 ready!"

Exploring Autonomously:
  → Rolling forward... *occasional happy beeps*
  ⚠️  Obstacle detected! *worried beeps*
  🔄 *Head shake nervously*
  ⏪ Backing up... *cautious beeps*
  👀 Scanning left... *beep*
  👀 Scanning right... *beep*
  ↺ Turning left! *happy beep*
  → Clear path ahead! *continues exploring*
```

---

## 🛠️ Hardware Requirements

### Main Components

| Component | Quantity | Notes |
|-----------|----------|-------|
| **Arduino Uno** | 1 | ATmega328P microcontroller |
| **Roinco Motor Shield V1.0** | 1 | L298N-based motor driver |
| **DC Motors** | 2 | 6-12V geared motors |
| **Servo Motor (SG90)** | 1 | For head scanning (0-180°) |
| **HC-SR04 Ultrasonic** | 1 | Distance sensor |
| **HC-05 Bluetooth Module** | 1 | Wireless communication |
| **IR Sensors** | 2 | For line following |
| **Buzzer** | 1 | Passive or active buzzer |
| **Battery** | 1 | 7.4V Li-Po 2S or 9V (2A min) |
| **Wheels** | 2 | Compatible with motors |
| **Chassis** | 1 | Robot body/frame |

### Optional Components
- Caster wheel or ball bearing (for stability)
- Power switch
- LED indicators
- Battery holder

### Electronic Components
- **1kΩ Resistor** (for voltage divider - optional)
- **2kΩ Resistor** (for voltage divider - optional)
- Jumper wires (male-to-male, male-to-female)
- Breadboard (optional, for prototyping)

---

## 🔌 Wiring Diagram

### Pin Configuration

```
Arduino Uno Pins:
├── D2  → Roinco IN1 (Left Motor Direction 1)
├── D3  → Roinco IN2 (Left Motor Direction 2)
├── D4  → Roinco IN3 (Right Motor Direction 1)
├── D5  → Roinco IN4 (Right Motor Direction 2)
├── D7  → Servo Signal (Orange/Yellow wire)
├── D8  → Ultrasonic Trigger & Echo (combined)
├── D9  → Buzzer (+)
├── D10 → Bluetooth RX (HC-05 TX)
├── D11 → Bluetooth TX (HC-05 RX)
├── D12 → IR Sensor Left (OUT)
└── D13 → IR Sensor Right (OUT)
```

### Detailed Wiring

#### Motor Connections
```
Roinco Motor Shield:
  OUT1, OUT2 ←→ Left Motor (Red & Black)
  OUT3, OUT4 ←→ Right Motor (Red & Black)

Arduino to Roinco:
  D2 → IN1
  D3 → IN2
  D4 → IN3
  D5 → IN4
```

#### Servo Motor (D7)
```
Servo SG90:
  Orange/Yellow → D7
  Red           → 5V
  Brown/Black   → GND
```

#### Ultrasonic Sensor (D8)
```
HC-SR04:
  VCC  → 5V
  TRIG → D8
  ECHO → D8 (same pin!)
  GND  → GND
```

#### Bluetooth Module (D10, D11)

**Option 1: Simple Wiring (3.3V power)**
```
HC-05:
  VCC → 3.3V (Arduino 3.3V pin)
  GND → GND
  TX  → D10 (direct)
  RX  → D11 (direct - no resistors!)
```

**Option 2: With Voltage Divider (5V power)**
```
HC-05:
  VCC → 5V
  GND → GND
  TX  → D10 (direct)
  RX  → Voltage Divider:
        D11 ─[1kΩ]─┬─ HC-05 RX
                   │
                 [2kΩ]
                   │
                  GND
```

#### IR Sensors (D12, D13)
```
Left IR Sensor:
  VCC → 5V
  GND → GND
  OUT → D12

Right IR Sensor:
  VCC → 5V
  GND → GND
  OUT → D13
```

#### Buzzer (D9)
```
Buzzer:
  (+) → D9
  (-) → GND
```

#### Power
```
Battery (7-12V):
  (+) → Roinco Shield Power (+)
  (-) → Roinco Shield Power (-)

⚠️ CRITICAL: All GND must be connected together!
```

### Visual Wiring Diagram

```
        ┌─────────────────────────────────┐
        │      ARDUINO UNO + ROINCO       │
        │                                 │
        │  [D2][D3][D4][D5]              │
        │     ↓   ↓   ↓   ↓               │
        │  [IN1][IN2][IN3][IN4]          │
        │                                 │
        │  [OUT1-OUT2]  [OUT3-OUT4]      │
        │       ↓              ↓           │
        │   Left Motor    Right Motor     │
        │                                 │
        │  D7────→ Servo                  │
        │  D8────→ Ultrasonic             │
        │  D9────→ Buzzer                 │
        │  D10───→ BT RX                  │
        │  D11───→ BT TX                  │
        │  D12───→ IR Left                │
        │  D13───→ IR Right               │
        │                                 │
        │  3.3V/5V → Sensors              │
        │  GND ────→ Common Ground        │
        └─────────────────────────────────┘
```

---

## 📥 Installation

### Step 1: Clone Repository
```bash
git clone https://github.com/yourusername/r2d2-arduino-robot.git
cd r2d2-arduino-robot
```

### Step 2: Hardware Assembly
1. Mount motors on chassis
2. Install Roinco Motor Shield on Arduino Uno
3. Connect motors to shield (OUT1-OUT4)
4. Wire control pins (D2-D5) from Arduino to shield
5. Mount servo on front for head scanning
6. Attach ultrasonic sensor to servo
7. Connect all sensors according to wiring diagram
8. Mount buzzer for audio feedback
9. Install IR sensors at front bottom (for line following)
10. Connect battery to Roinco shield power terminals

### Step 3: Upload Code
1. Open `R2D2_ROBOT_FIXED.ino` in Arduino IDE
2. Select **Tools → Board → Arduino Uno**
3. Select **Tools → Port → [Your Arduino Port]**
4. Click **Upload** (→ button)
5. Wait for "Upload Complete" message

### Step 4: Test
1. Open **Serial Monitor** (Tools → Serial Monitor)
2. Set baud rate to **9600**
3. You should see R2-D2 startup message
4. Hear startup sequence: excited beeps + head shake + whistle

---

## 🎮 Usage

### Serial Monitor Control (USB)

1. **Connect** Arduino via USB
2. **Open** Serial Monitor (9600 baud)
3. **Type** commands and press Enter

Example:
```
Type: F → Robot moves forward
Type: 2 → Servo looks center
Type: A → Auto mode activated!
Type: H → R2-D2 happy sounds!
```

### Bluetooth Control (Wireless)

#### Pairing HC-05
1. **Power on** robot
2. **Enable Bluetooth** on smartphone
3. **Search** for devices → Find "HC-05" or "HC-06"
4. **Pair** with device (PIN: `1234` or `0000`)

#### Recommended Apps
**Android:**
- Serial Bluetooth Terminal
- Arduino Bluetooth Controller
- Bluetooth Electronics

**iOS:**
- BLE Terminal
- Arduino Bluetooth (limited support)

#### Sending Commands
1. **Connect** to HC-05 in app
2. **Send** single character commands (F, B, L, R, etc.)
3. **Watch** R2-D2 respond with beeps and movement!

---

## 🎭 R2-D2 Personality

### Sound Effects

| Situation | Sound | Description |
|-----------|-------|-------------|
| **Power On** | 🎵 Excited beeps | Rising tones: beep-beep-BEEP! |
| **Happy** | 😊 Beep-boop-beep | High-low-high cheerful sound |
| **Worried** | 😟 Boop-boop-boop | Fast low-pitched urgent beeps |
| **Confused** | 🤔 Random beeps | Mixed frequency confused sounds |
| **Whistle** | 🎶 Wheee-oooo | Long melodic tones |
| **Alert** | ⚠️ BEEP-BEEP-BEEP | Rapid high-pitched warning |
| **Acknowledge** | ✅ Beep-boop | Quick confirmation sound |

### Movements

| Action | Behavior | When It Happens |
|--------|----------|-----------------|
| **Head Shake** | Rapid left-right oscillation | Worried, excited, or confused |
| **Head Nod** | Up-down movement | Acknowledging commands |
| **Cautious Scan** | Slow left-center-right | Looking for obstacles |
| **Random Beeps** | Occasional chirps | When rolling happily |

### Emotional States

```python
State: HAPPY
├─ Clear path ahead
├─ Successfully avoided obstacle
└─ Sounds: High beeps, occasional chirps
   Movement: Smooth forward motion

State: WORRIED
├─ Obstacle detected
├─ Both paths blocked
└─ Sounds: Low rapid beeps
   Movement: Head shake, backup

State: EXCITED
├─ Starting auto mode
├─ New adventure begins
└─ Sounds: Rising beeps, whistle
   Movement: Head shake

State: CAUTIOUS
├─ Approaching obstacle
├─ Scanning environment
└─ Sounds: Careful beeps
   Movement: Slow scan left-right
```

---

## 🕹️ Commands

### Movement Commands

| Command | Action | R2-D2 Response |
|---------|--------|----------------|
| `F` or `f` | Move Forward | 🎵 Forward beep |
| `B` or `b` | Move Backward | 🎵 Backward beep |
| `L` or `l` | Turn Left | 🎵 Turn beep |
| `R` or `r` | Turn Right | 🎵 Turn beep |
| `S` or `s` | Stop Motors | 🎵 Stop beep |

### Mode Commands

| Command | Mode | R2-D2 Response |
|---------|------|----------------|
| `A` or `a` | Auto Mode (Obstacle Avoidance) | 🎉 Excited beeps + "Exploring!" |
| `T` or `t` | Line Follow Mode | 😊 Happy beeps + "Following line!" |
| `M` or `m` | Manual Mode | ✅ Acknowledge beep + "Manual mode" |

### Servo Commands

| Command | Servo Position | Angle |
|---------|---------------|-------|
| `1` | Look Left | 150° |
| `2` | Look Center | 90° |
| `3` | Look Right | 30° |

### Special Commands

| Command | Action | R2-D2 Response |
|---------|--------|----------------|
| `H` or `h` | Happy Sound + Nod | 😊 Beep-boop-beep! + head nod |
| `W` or `w` | R2-D2 Whistle | 🎶 Wheee-oooo! |
| `0` | Emergency Stop | ⚠️ Alert beeps + stop all |

---

## 🎯 Modes

### 1. Manual Mode (Default)
**Activation:** Press `M` or power on robot

**Behavior:**
- Robot responds to directional commands (F/B/L/R)
- You have full control
- R2-D2 beeps with each command
- Servo can be controlled independently

**Use Case:** Direct control, testing, specific maneuvers

---

### 2. Auto Mode (Obstacle Avoidance)
**Activation:** Press `A`

**Behavior:**
1. Robot drives forward automatically
2. Continuously measures distance ahead
3. **When obstacle detected (<20cm):**
   - 😟 Worried beeps
   - 🔄 Stops and shakes head
   - ⏪ Backs up
   - 👀 Scans left (150°)
   - 👀 Scans right (30°)
   - 🧠 Decides clearest path
   - ↺/↻ Turns toward clear direction
   - ✅ Acknowledge beep, continues
4. **When path clear:**
   - 😊 Occasional happy beeps
   - → Continues forward

**Algorithm:**
```
LOOP:
  measure_distance()
  
  IF distance < 20cm:
    worried_beeps()
    stop()
    backup()
    head_shake()
    
    scan_left()
    measure_left_distance()
    
    scan_right()
    measure_right_distance()
    
    IF left_clearer AND left_safe:
      turn_left()
      happy_beep()
    ELSE IF right_safe:
      turn_right()
      happy_beep()
    ELSE:
      confused_beeps()
      turn_around_180()
    
    acknowledge_beep()
    
  ELSE IF distance < 30cm:
    cautious_beep()
    move_forward()
    
  ELSE:
    move_forward()
    random_happy_beep()
```

**Use Case:** Autonomous exploration, maze navigation, demonstrations

---

### 3. Line Follow Mode
**Activation:** Press `T`

**Behavior:**
1. Robot follows black line on white surface
2. **Both IR sensors on line:** → Move straight
3. **Left sensor on line:** ↺ Turn left
4. **Right sensor on line:** ↻ Turn right  
5. **Both sensors off line:** ⚠️ Stop + worried beeps

**IR Sensor Logic:**
```
┌─────────────────────────────────┐
│  LEFT IR    RIGHT IR    ACTION  │
├─────────────────────────────────┤
│  ● Black    ● Black     ↑ Fwd   │
│  ● Black    ○ White     ↺ Left  │
│  ○ White    ● Black     ↻ Right │
│  ○ White    ○ White     ■ Stop  │
└─────────────────────────────────┘
```

**Track Setup:**
- Use black electrical tape on white surface
- Line width: 2-3cm
- IR sensors: 1-2cm above ground, 5cm apart
- Track curves: Gentle (not sharp 90° turns)

**Use Case:** Line following competitions, guided paths, delivery routes

---

## 🔧 Troubleshooting

### Servo Not Moving

**Problem:** Servo head doesn't scan

**Solutions:**
1. ✓ Check signal wire connected to **D7**
2. ✓ Verify **5V** and **GND** connected to servo
3. ✓ Test with Serial Monitor: Type `2` → should center
4. ✓ Check servo not mechanically stuck
5. ✓ Try different servo (might be damaged)
6. ✓ Ensure sufficient power (battery connected)

---

### Motors Don't Spin

**Problem:** No movement when commands sent

**Solutions:**
1. ✓ Check battery connected to Roinco shield
2. ✓ Verify battery voltage: 7-12V
3. ✓ Ensure D2-D5 connected to Roinco IN1-IN4
4. ✓ Check motor wires tight in screw terminals
5. ✓ Test with Serial Monitor: Type `F`
6. ✓ If one motor wrong direction: swap its two wires

---

### Bluetooth Not Working

**Problem:** Can't pair or receive commands

**Check LED Status:**
```
Blinking fast (not paired)  → Normal, try pairing
Blinking slow (paired)      → Good! Send commands
Not blinking at all         → Power problem
```

**Solutions:**
1. ✓ Check HC-05 **VCC** → 3.3V or 5V
2. ✓ Check HC-05 **GND** → Arduino GND
3. ✓ Check HC-05 **TX** → Arduino D10
4. ✓ Check HC-05 **RX** → Arduino D11
5. ✓ If using 5V power: **voltage divider required!**
6. ✓ Try pairing PIN: `1234` or `0000`
7. ✓ Check phone Bluetooth is ON
8. ✓ Upload BLUETOOTH_TEST.ino to diagnose
9. ✓ Try different baud rate: `bluetooth.begin(38400);`

**Voltage Divider Check (if using 5V):**
```
D11 ─[1kΩ]─┬─ HC-05 RX  ← Must have this!
           │
         [2kΩ]
           │
          GND
```

---

### Ultrasonic Not Detecting

**Problem:** Robot doesn't avoid obstacles

**Solutions:**
1. ✓ Check **Trig** and **Echo** both to **D8**
2. ✓ Verify **VCC** → 5V, **GND** → GND
3. ✓ Open Serial Monitor, press `A`
4. ✓ Should see "Distance: XX cm" messages
5. ✓ If distance always 0 or 400: sensor issue
6. ✓ Ensure nothing blocking sensor face
7. ✓ Try different ultrasonic sensor

---

### No Sound from Buzzer

**Problem:** R2-D2 is silent

**Solutions:**
1. ✓ Check buzzer **( +)** → **D9**
2. ✓ Check buzzer **(-)** → **GND**
3. ✓ Try swapping buzzer polarity (if passive)
4. ✓ Test: Type `H` in Serial Monitor
5. ✓ Should hear 3 beeps
6. ✓ If still silent: try different buzzer

---

### IR Sensors Not Working

**Problem:** Line following doesn't work

**Solutions:**
1. ✓ Check **Left IR OUT** → **D12**
2. ✓ Check **Right IR OUT** → **D13**
3. ✓ Verify **VCC** → 5V, **GND** → GND for both
4. ✓ Sensors 1-2cm above ground
5. ✓ Test on black line: LED on sensor should light up
6. ✓ Adjust sensor height/sensitivity potentiometer
7. ✓ Ensure line is actually black (dark enough)

---

### Robot Drifts to One Side

**Problem:** Doesn't go straight

**Solutions:**
1. ✓ Motors might have different speeds
2. ✓ Check both motors getting power
3. ✓ Adjust wheel alignment
4. ✓ Add small delays to compensate:
   ```cpp
   void moveForward() {
     digitalWrite(MOTOR_A_DIR1, HIGH);
     digitalWrite(MOTOR_A_DIR2, LOW);
     delay(5);  // Add delay for slower motor
     digitalWrite(MOTOR_B_DIR1, HIGH);
     digitalWrite(MOTOR_B_DIR2, LOW);
   }
   ```

---

### Power Issues

**Problem:** Robot works on USB but not on battery

**Solutions:**
1. ✓ Check battery voltage: 7-12V required
2. ✓ Check battery charged (use multimeter)
3. ✓ Verify battery connected to Roinco shield
4. ✓ Ensure power switch ON (if installed)
5. ✓ Check all GND connected together
6. ✓ Battery must provide 2A minimum current

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Ways to Contribute
- 🐛 Report bugs
- 💡 Suggest new features
- 📝 Improve documentation
- 🎨 Add new R2-D2 sounds/movements
- 🔧 Submit bug fixes
- ⭐ Star the project!

### Pull Request Process
1. Fork the repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### Code Style
- Use meaningful variable names
- Comment complex logic
- Follow existing code structure
- Test thoroughly before submitting

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 [Your Name]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Acknowledgments

### Inspiration
- **Star Wars** - For creating the iconic R2-D2 character
- **Arduino Community** - For extensive tutorials and support
- **Open Source Robotics** - For sharing knowledge freely

### Libraries Used
- `Servo.h` - Arduino servo control
- `SoftwareSerial.h` - Software serial communication

### Resources
- [Arduino Official Documentation](https://www.arduino.cc/)
- [HC-05 Bluetooth Module Guide](https://components101.com/wireless/hc-05-bluetooth-module)
- [L298N Motor Driver Tutorial](https://lastminuteengineers.com/l298n-dc-stepper-driver-arduino-tutorial/)

### Special Thanks
- Arduino team for the amazing platform
- All contributors who helped improve this project
- The maker community for inspiration and support

---

## 📞 Contact

**Project Maintainer:** [Your Name]

- GitHub: [@yourusername](https://github.com/yourusername)
- Email: your.email@example.com
- Project Link: [https://github.com/yourusername/r2d2-arduino-robot](https://github.com/yourusername/r2d2-arduino-robot)

---

## 🌟 Show Your Support

If you like this project, please:
- ⭐ Star the repository
- 🍴 Fork and create your own version
- 📢 Share with friends
- 🐛 Report issues
- 💬 Give feedback

---

## 📸 Gallery

### Robot Assembly
```
[Add photos of your assembled robot here]
- Front view
- Side view
- Wiring close-up
- In action
```

### Demo Videos
```
[Add links to demo videos]
- Auto mode demonstration
- Line following
- Bluetooth control
- R2-D2 sounds showcase
```

---

## 🗺️ Roadmap

### Current Version: v1.0
- ✅ Basic obstacle avoidance
- ✅ Line following
- ✅ Bluetooth control
- ✅ R2-D2 sounds and movements

### Future Enhancements
- 🔲 Add more R2-D2 sound variations
- 🔲 Implement voice recognition
- 🔲 Add LED matrix for "eye" display
- 🔲 Improve AI decision making
- 🔲 Add mobile app with custom UI
- 🔲 Integrate accelerometer for balance
- 🔲 Add obstacle mapping
- 🔲 Implement return-to-base feature

---

## 📚 Additional Resources

### Tutorials
- [Getting Started with Arduino](https://www.arduino.cc/en/Guide/HomePage)
- [Motor Control Basics](https://www.arduino.cc/en/Tutorial/LibraryExamples/MotorKnob)
- [Bluetooth Communication](https://create.arduino.cc/projecthub/mayoogh/bluetooth-controlled-car-a4c44f)

### Datasheets
- [Arduino Uno Datasheet](https://www.arduino.cc/en/uploads/Main/Arduino_Uno_Rev3-schematic.pdf)
- [L298N Motor Driver](https://www.sparkfun.com/datasheets/Robotics/L298_H_Bridge.pdf)
- [HC-05 Bluetooth](https://components101.com/sites/default/files/component_datasheet/HC-05%20Datasheet.pdf)
- [HC-SR04 Ultrasonic](https://cdn.sparkfun.com/datasheets/Sensors/Proximity/HCSR04.pdf)

---

## ❓ FAQ

**Q: Can I use Arduino Mega instead of Uno?**
A: Yes! Just update pin definitions in code.

**Q: What's the maximum range of Bluetooth?**
A: HC-05 typically has 10-30 meters range (clear line of sight).

**Q: Can I add more sensors?**
A: Yes! Use available analog pins or I2C sensors.

**Q: Does it work without Bluetooth?**
A: Yes! Use Serial Monitor via USB cable.

**Q: Can I customize R2-D2 sounds?**
A: Absolutely! Edit the `tone()` frequencies and durations in code.

**Q: What battery life can I expect?**
A: Depends on battery capacity. 2000mAh typically gives 1-2 hours.

---

<div align="center">

### Made with ❤️ and lots of beep-boops!

**May the Force be with you!** ⭐

</div>
