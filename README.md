# 🧠 Neuro-Dungeon: Teaching Embodied AI with LLMs

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](YOUR_COLAB_LINK_HERE)
[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![Model](https://img.shields.io/badge/Model-GPT--4o--mini-green)](https://openai.com/)
[![License](https://img.shields.io/badge/License-MIT-purple)](LICENSE)

## 📖 Project Overview

**Neuro-Dungeon** is a pedagogical framework designed to bridge the gap between traditional Game AI and modern **Robotics**. Unlike scripted NPCs using Finite State Machines, this project implements a **Vision-Language-Action (VLA)** model.

The agent navigates a procedurally generated dungeon not by following hard-coded rules, but by **reasoning** about its sensory data using a Large Language Model (`gpt-4o-mini`).

> **"From Chatbots to Agents: Don't just talk, ACT."**

This project demonstrates the **"Symbol Grounding Problem"**: How do we translate high-level semantic intent ("Find the flag") into low-level executable actions (`MOVE_UP`, `MOVE_DOWN`)?

## 🎯 Key Features

* **Simulated Edge Computing:** Utilizes `gpt-4o-mini` to simulate a resource-constrained environment typical in robotics, prioritizing low-latency inference over massive context windows.
* **Embodied Perception:** The agent does not have "God Mode." It relies on a **3x3 Local Lidar View** and a **Signal Strength (Distance)** metric, requiring it to build an internal mental map (SLAM).
* **Explainable AI (XAI):** Features a "Black Box Analysis" module that logs the agent's **Chain-of-Thought (CoT)**, allowing students to audit *why* a specific move was chosen.
* **Neuro-Symbolic Architecture:** Combines the probabilistic reasoning of LLMs with the deterministic physics of a grid-based game engine.

## 🏗️ System Architecture

The project structure maps classical robotics components to game development classes:

| Robotics Module | Game Context | Function |
| :--- | :--- | :--- |
| **World Simulator** | `AdvancedDungeon` | Manages Physics, Collision, and Procedural Generation. |
| **Lidar/Sensors** | `get_local_view()` | Raycasting simulation; converts grid state to ASCII text. |
| **Planner (Brain)** | `RealLLMBrain` | The VLA model. Processes text sensors -> Outputs JSON plan. |
| **Actuator** | `step()` | Parses JSON and executes atomic movements. |

### The Reasoning Loop

```mermaid
graph LR
    A[Environment] -->|1. Local View & Distance| B(LLM Brain)
    B -->|2. Chain of Thought| C{Decision Module}
    C -->|3. JSON Command| D[Actuator]
    D -->|4. Update State| A