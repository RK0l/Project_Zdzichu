# Project Zdzichu

**Zdzichu** is a modular, voice-first AI assistant designed to provide natural, continuous conversation while also controlling and monitoring a smart home.

The primary goal is not simply to create another voice-command system, but to build an assistant that feels natural to talk to — understands context, allows interruptions, responds quickly and can perform actions in the home when appropriate.

## 🎯 Project Goals

The assistant should be able to:

* respond to the wake word **"OK Zdzichu"**
* understand natural spoken language
* maintain conversational context
* conduct a free-form conversation
* be interrupted while speaking
* react immediately to the user's speech
* control devices and scenes through **Home Assistant**
* provide information about the state of the home
* distinguish between conversation and commands
* operate using replaceable AI/STT/TTS components

The system should prioritize **responsiveness, natural interaction and reliability** over simply using the newest or largest AI model.

---

## 🧠 Core Architecture

Project Zdzichu is designed as a modular system.

```text
                ┌─────────────────────┐
                │      User Voice     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │      Wake Word      │
                │    "OK Zdzichu"     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │         STT         │
                │   Speech → Text     │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │    ORCHESTRATOR     │
                │                     │
                │  Conversation Flow │
                │  Context           │
                │  Interruptions     │
                │  Actions           │
                └──────┬───────┬──────┘
                       │       │
              ┌────────┘       └────────┐
              ▼                         ▼
      ┌───────────────┐        ┌────────────────┐
      │      LLM      │        │ Home Assistant │
      │ Conversation  │        │    Control     │
      └───────┬───────┘        └────────────────┘
              │
              ▼
      ┌───────────────┐
      │      TTS      │
      │ Text → Speech │
      └───────┬───────┘
              │
              ▼
         🔊 Assistant
```

### Main Components

**Wake Word**
Detects the phrase "OK Zdzichu" and activates the assistant.

**STT — Speech to Text**
Converts the user's speech into text.

**LLM — Large Language Model**
Responsible for understanding language, maintaining conversation and determining the user's intent.

**Orchestrator**
The central component of the system. It controls the complete conversation flow and connects all other modules.

The orchestrator should handle:

* listening
* thinking
* speaking
* interruptions
* conversation context
* LLM communication
* Home Assistant actions
* errors and timeouts

**TTS — Text to Speech**
Converts the assistant's response into speech.

**Home Assistant Integration**
Provides controlled access to the smart home.

The LLM should **not directly control the home**. Actions should pass through the orchestrator and defined interfaces.

---

## ⚡ Key Requirement: Natural Conversation

A major objective of Project Zdzichu is to avoid the traditional voice-assistant model:

> Listen → wait → generate entire response → speak entire response → listen again

Instead, the system should support:

* streaming responses
* streaming TTS
* immediate playback
* speech interruption
* automatic detection that the user has started speaking
* cancellation of the current response
* returning to listening without restarting the entire conversation

The feeling should be closer to a real conversation.

---

## 🏠 Home Assistant

Home Assistant will be the primary home-automation platform.

Initial capabilities may include:

* lights
* switches
* scenes
* blinds / shutters
* temperature
* sensors
* device status
* predefined routines

Example:

> "OK Zdzichu, zgaś światło w salonie."

or:

> "OK Zdzichu, przygotuj dom do snu."

The second command may trigger multiple actions while still being treated as one natural user request.

---

## 🔌 Modular Design

Every major component should be replaceable.

Possible future replacements:

* STT model
* TTS engine
* LLM
* wake-word engine
* audio input/output
* Home Assistant interface

Changing one component should not require rebuilding the entire system.

---

## 🛠 Development Strategy

Development will be incremental.

### v0.1 — Conversation Prototype

* [ ] Basic audio input
* [ ] STT
* [ ] LLM connection
* [ ] TTS
* [ ] Basic conversation
* [ ] Measure response latency

### v0.2 — Real-time Conversation

* [ ] Streaming LLM responses
* [ ] Streaming TTS
* [ ] Speech interruption
* [ ] Voice Activity Detection
* [ ] Conversation cancellation
* [ ] "OK Zdzichu" wake word

### v0.3 — Home Assistant

* [ ] Home Assistant connection
* [ ] Read entity states
* [ ] Control lights
* [ ] Control switches
* [ ] Execute scenes
* [ ] Safe action handling

### v0.4 — Context

* [ ] Conversation memory
* [ ] Context-aware commands
* [ ] Follow-up questions
* [ ] Multi-step commands

### v1.0 — Zdzichu

A stable voice assistant capable of natural conversation and reliable smart-home control.

---

## 📁 Planned Project Structure

```text
project-zdzichu/
│
├── README.md
├── docs/
├── orchestrator/
├── stt/
├── tts/
├── llm/
├── wakeword/
├── homeassistant/
├── audio/
├── config/
└── tests/
```

The exact structure may change during development.

---

## 🚧 Current Status

**Project stage:** Planning / Architecture

The first objective is to build a working conversational prototype before adding extensive Home Assistant functionality.

---

## 📌 Design Philosophy

> **Zdzichu should behave like an assistant you can talk to, not a device that waits for commands.**

Responsiveness and natural interaction are considered first-class features of the project.
