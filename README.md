# Smart Home Controller with Generative AI

## Introduction

This project simulates a smart home environment where users can control and monitor virtual devices using natural language commands. Instead of using buttons or menus, users simply type commands like:

- “Turn on the light.”
- “Set the fan speed to high.”
- “What is the current temperature?”

These commands are interpreted using a Generative AI model (OpenAI GPT), which converts them into structured actions that the system executes using Python classes.

---

## Step 1: Simulating Smart Home Devices

We define three Python classes to simulate smart devices:

### Light
- Can be turned ON or OFF.
- `get_status()` returns the current state.

### Fan
- Can be turned ON or OFF.
- Supports speed settings: `low`, `medium`, `high`.
- `get_status()` returns the current state and speed.

### Thermostat
- Allows temperature setting between 18°C and 30°C.
- `get_status()` returns the current temperature.

Each class maintains its own state and supports basic control methods.

---

## Step 2: Command Parsing with Generative AI

To process natural language commands, we use OpenAI's `gpt-3.5-turbo` model. The model receives user input and returns a structured JSON object.

### Example

**User Input**:  

Set the fan speed to high


**AI Output**:  
```json
{
  "device": "fan",
  "action": "set_speed",
  "value": "high"
}

```

The system expects three fields:

- device: the target device (light, fan, or thermostat)

- action: the command (e.g., turn_on, set_temperature)

- value: optional value (e.g., temperature or fan speed)

---
## Step 3: Command Execution and Feedback

The `execute_command()` function receives the parsed JSON and calls the appropriate method on the device class.

### What it does:
- Maps the device, action, and value to a Python method
- Executes the command (e.g., turning on the fan)
- Returns a user-friendly response

### Example Output:
"The fan speed is set to high."


### Benefits:
- Modular: Easy to add new devices or actions
- Flexible: Accepts both strings and dictionaries
- Safe: Includes error handling

---

## Step 4: Command-Line Interface (CLI)

A simple CLI allows users to type natural language commands in real time.

### Example Interaction

Welcome to your Smart Home! Type a command (or type 'exit' to quit)

You: Set the fan speed to high
AI Parsed: {"device": "fan", "action": "set_speed", "value": "high"}
Smart Home: The fan speed is set to high.

You: What is the temperature?
AI Parsed: {"device": "thermostat", "action": "get_status"}
Smart Home: The thermostat is set to 22°C.

You: exit
Exiting Smart Home. Goodbye!



---

## Sample Commands and Expected Outputs

| Command                         | Expected Output                          |
|--------------------------------|-------------------------------------------|
| Turn on the light              | The light is now ON.                      |
| Turn off the fan               | The fan is now OFF.                       |
| Set the fan speed to medium    | The fan speed is set to medium.           |
| Set the thermostat to 25°C     | The thermostat is set to 25°C.            |
| What is the status of all devices? | The light is ON. The fan is OFF. The thermostat is set to 22°C. |

---

## Technologies Used

- Python 3
- OpenAI GPT (via `openai` Python library)
- CLI using built-in `input()` function

