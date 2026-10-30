# ESP32-S3 Access Console

A local-first web console and offline AI assistant for ESP32-S3 close-access hardware, built with a **detection-engineering** focus. Every generated action is annotated with its MITRE ATT&CK technique, the host/EDR telemetry it produces, and a starter hunting query — pairing the offensive action with the defensive signal it generates.

> **Authorized use only.** This project is for security research and detection validation on systems you own or are explicitly contracted to test. HID keystroke injection maps to MITRE ATT&CK [T1200 (Hardware Additions)](https://attack.mitre.org/techniques/T1200/) and [T1091](https://attack.mitre.org/techniques/T1091/). Unauthorized use against systems you do not own is illegal under the UK Computer Misuse Act 1990 and equivalent legislation. The author accepts no liability for misuse.

## Why this exists

Most close-access tooling answers one question: *how do I run a payload?* This project answers a second one that matters more in a SOC/purple-team context: *what does this attack look like to the defender, and what's the rule to catch it?* The console is built so that generating an action always produces its detection story alongside it.

## Architecture

| Layer | Component |
|-------|-----------|
| Hardware | LilyGo T-Dongle S3 (ESP32-S3, native USB-OTG for HID) |
| Firmware | USB Army Knife (open source) |
| UI | This PWA — installable, offline-capable |
| AI | Local Ollama model, no cloud dependency |
| Output | DuckyScript **+** ATT&CK mapping + expected telemetry + hunt query |

The UI talks to the device over its Wi-Fi AP (default `192.168.4.1`) and to a local Ollama-backed service for AI generation. Nothing leaves the host.

## Repository contents

- `index.html` — the PWA console (tabs: Scripts, Recon, AI, Tools, Settings). Runs standalone in any browser; the simulator and preset library need no hardware.
- `docs/build-guide.html` — full build guide: bill of materials, firmware flashing, and the local AI assistant setup.

## Scope note

The preset library ships benign, telemetry-generating actions intended for detection labs — launch-a-process, type-a-marker, local host inventory. It deliberately does not ship weaponized payloads; the device executes whatever the operator loads, and real engagements use established tooling for that.

## Status

Active development. Software layer (UI, simulator, local AI integration) is functional; firmware flashing and device endpoint verification require the hardware.
