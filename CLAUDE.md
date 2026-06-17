# UNO Q AI Starter Kit — Project Documentation

## Project Overview

This is the documentation and course repository for the **SunFounder AI Starter Kit with Arduino Uno Q** (UNO Q AIoT Learning Kit). The kit targets beginners aged 10+, students, educators, and makers. Through hardware experiments, IoT applications, and AI technology practices, learners progress from basic hardware control to IoT systems to AI-powered devices.

- **GitHub**: sunfounder/inventor-lab-kit
- **Docs engine**: Sphinx (RST format, sphinx_rtd_theme)
- **Source**: `docs/source/`
- **Audience**: Beginners with zero programming or electronics experience
- **Language**: English

## Hardware Platform

- **Board**: Arduino UNO Q (Qualcomm QRB2210 MPU + STM32U585 MCU, dual-processor)
- **Expansion**: Robot Shield (battery management, motor/servo drivers, multi-rail power, onboard MCU)
- **Multimedia**: Multimedia Carrier (dual CSI cameras, DSI display, microphone, speaker, headphone jack, RGB LEDs, 10-axis IMU)
- **Sensors**: Ultrasonic, DHT11, photoresistor, thermistor, PIR motion sensor
- **Actuators**: Servos (×2, metal gear), DC motor + fan, active/passive buzzers, RGB LED, LEDs
- **Input**: Joystick, potentiometer, tilt switch, buttons
- **Components**: Breadboard, resistors (10Ω–1MΩ), transistors (NPN/PNP), capacitors, jumper wires

## Software Platform

- **Arduino App Lab**: Web-based IDE — the primary development tool for this course. No driver installation needed. Students create/edit/import/run apps in a browser-like environment.
- **Arduino IDE**: Introduced in a comparison lesson (Module A, lesson 13).
- **Edge Impulse**: Used in Module D for AI model training and deployment.
- **LLM Integration**: Module C connects to Gemini/ChatGPT for AI-driven hardware interaction.

## Course Structure (4 Modules, ~34 Lessons)

| Module | Lessons | Theme |
|--------|---------|-------|
| A: Basic Interaction | 13 | Digital I/O, analog, PWM, sensors, actuators |
| B: UI / Cloud / IoT | 7 | Web UI, Arduino Cloud, Telegram Bot |
| C: AI & LLM | 4 | Gemini/ChatGPT integration, AI-controlled hardware |
| D: Edge AI | 10 | Vision, voice, Edge Impulse, custom models |

### Module A Lesson Order (Finalized)

1. Hello LED — digital output
2. Button LED — digital input
3. Tilt Alarm — digital input + active buzzer
4. Potentiometer LED — analog input + PWM (newly added)
5. RGB LED — PWM color mixing
6. Photoresistor Night Light — analog sensor + conditionals
7. DHT11 — first library-based sensor
8. Ultrasonic Radar — timing-based sensor
9. Thermistor Fan — analog input + PWM motor
10. Joystick LED — dual-axis analog
11. Servo Pan-Tilt — servo library
12. IMU Attitude — I2C + complex sensor
13. IDE Comparison — App Lab vs Arduino IDE

**Pedagogical principle**: Each lesson introduces at most one genuinely new concept. Everything else builds on previously learned knowledge, so students feel "I already know this, just one small new thing."

## Lesson Template

Every lesson follows this fixed structure. The numbered sections (1–5) let students follow along without thinking about what to do next.

```
Lesson Title
============

Introduction
    - Brief concept primer (1–2 paragraphs). Explain unfamiliar terms
      BEFORE the student touches hardware (e.g., "What is an LED?").
    - Learning objectives (bullet list, 3–5 items).

1. Build the Circuit
    - Components Needed: 4-column table using |list_xxx| image substitutions.
      No header row. Each component gets a picture.
    - Wiring Diagram: Fritzing breadboard view. Text describes electrical
      connections only (not physical hole positions). The diagram owns
      physical placement.
    - Circuit Diagram: Schematic. Shows the same circuit in electrical
      notation. Include current flow path explanation.

2. Code
    - Import the Code: Standardized workflow for every lesson —
      Import App → navigate to unoq-ai-kit/<module>/ → select <lesson>.zip
    - Run the Code: Click Run → wait → observe the result.
    - The Code: Show the complete code (AFTER the student has seen it work).
    - How it Works: Walk through each function/concept. Student is now
      curious because they've already seen the result.

3. Experiment
    - Guided modifications with a table showing input → effect.
    - At least one challenge with complete code provided (not just hints).
    - Advanced challenge with collapsible solution.

4. Troubleshooting
    - Cause/Solution format (not a table). Each issue is a bold heading
      followed by Cause: and Solution: lines.
    - Cover: wiring mistakes, wrong components, upload issues, burnout.

5. Summary
    - Bullet list of what was learned (3–5 items).
    - Next lesson teaser.
```

## Writing Conventions

### Diagrams
- **Fritzing** (`*_fritzing.png`): Breadboard wiring. Text steps describe electrical connections only — never reference specific breadboard hole numbers. The diagram is the single source of truth for physical placement.
- **Schematic** (`*_schematic.png`): Electrical notation. Use the same reference designators as the Fritzing diagram.

### Code
- All code is delivered as `.zip` files for import into App Lab. The import workflow is identical across all lessons.
- Code blocks use `.. code-block:: cpp` with `:linenos:`.
- Show complete code once, after the student has run it and seen the result.

### Components
- Use `.. list-table::` with `|list_xxx|` image substitutions (defined in `conf.py`).
- 4 columns, no header row, 25/25/25/25 width ratio.
- Components that span rows (like Arduino) can appear alone in a row.

### Tone
- Conversational, encouraging, direct. Use "you" and "your".
- Explain why, not just what. Every component choice has a reason.
- Celebrate milestones ("You just built your first working circuit!").

### Images
- Placeholder naming: `<lesson_number>_<description>.png`
- Example: `1_hello_led_fritzing.png`, `1_hello_led_schematic.png`, `1_blink_result.gif`
- Images referenced as `img/filename.png` (Sphinx resolves from source dir).

## File Organization

```
docs/source/
├── index.rst                    # Home page
├── conf.py                      # Sphinx config (substitutions, extensions)
├── 大纲.rst                     # Course outline (Chinese, authoritative)
├── faq.rst                      # FAQ
├── get_start/                   # Getting Started (before lessons)
│   ├── get_start.rst
│   ├── uno_q.rst
│   ├── robot_shield.rst
│   ├── app_lab.rst
│   ├── first_app.rst
│   └── arduino_ide.rst
├── basic/                       # Module A: Basic Interaction
│   ├── basic.rst                # Module index + toctree
│   └── <n>_<lesson_name>.rst    # Individual lessons (1–13)
├── iot/                         # Module B: IoT (planned)
├── ai/                          # Module C: AI/LLM (planned)
├── edge_ai/                     # Module D: Edge AI (planned)
└── _static/                     # Static assets
    ├── img/
    ├── video/
    ├── pdf/
    └── zip/
```

## Code Delivery Convention

All lesson code is distributed as `.zip` files organized by module:

```
unoq-ai-kit/
├── basic/
│   ├── 1_hello_led.zip
│   ├── 2_button_led.zip
│   └── ...
├── iot/
├── ai/
└── edge_ai/
```

The student imports these via: App Lab → Import App → navigate to folder → select `.zip`.
