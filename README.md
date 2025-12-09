# 🧠 Neuro-Dungeon: Teaching Embodied AI via Text Adventures

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_LINK_HERE)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)

## 📖 Project Overview

**Neuro-Dungeon** is a minimalist educational framework designed to teach core concepts of modern Robotics and Embodied AI—specifically **LLM-Based Task Planning**—using the accessible medium of a Text Adventure Game.

This project serves as a prototype for a **Vision-Language-Action (VLA)** model. Instead of relying on complex physics simulations, it abstracts the environment to focus purely on the **reasoning loop**: translating unstructured natural language observations into structured, executable JSON commands.

> **"From Chatbots to Agents: Don't just talk, ACT."**

## 🎯 Key Features

* **Pure Python Implementation:** Zero-dependency (standard library + matplotlib), lowering the barrier to entry for students.
* **Simulated Embodied Reasoning:** Demonstrates the "Grounding Problem"—how to map high-level semantic intent to low-level atomic actions.
* **Visual Debugging:** Includes a `matplotlib`-based grid visualization (simulating a SLAM map) to show the agent's state in real-time.
* **Pedagogy-First Design:** Features a "Mock LLM" module, allowing students to understand the architecture without requiring expensive API keys or GPUs.

## 🏗️ System Architecture

This project maps classical robotics control architectures onto game development components:

| Robotics Module | Game Context | Function |
| :--- | :--- | :--- |
| **World Simulator** | `DungeonWorld` Class | Maintains the Grid Map, collision rules, and physical state. |
| **Sensors (Lidar/Camera)** | `get_observation()` | Encodes the state into a Textual Description (Prompt). |
| **Planner (VLA Model)** | `llm_brain()` | Processes text and outputs a High-level Plan. |
| **Controller / Actuator** | `step(json)` | Parses JSON instructions and executes atomic actions (Move, Pick, Unlock). |

### The Reasoning Loop

```mermaid
graph LR
    A[Environment] -->|1. Text Observation| B(LLM / Brain)
    B -->|2. Reasoning| C{Decision Module}
    C -->|3. JSON Command| D[Actuator]
    D -->|4. State Update| A