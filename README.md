# OTAP: Open Tag Acquisition Project

[![Status: Early Development](https://img.shields.io/badge/status-early%20development-yellow)]()
[![Privacy: Edge-Only](https://img.shields.io/badge/privacy-local%20first-brightgreen)]()

**OTAP** is a local-first, in-vehicle computer vision system designed to detect, decode, and log license plate observations from live camera feeds. 

By operating entirely on edge hardware with no cloud dependencies, OTAP provides transparent, user-controlled visibility into vehicle-encountered license plate events without reliance on third-party infrastructure or subscription services.

---

## 📑 Table of Contents
* [Core Functionality](#core-functionality)
* [Design Philosophy](#design-philosophy)
* [Hardware Architecture](#hardware-architecture)
* [Data Privacy](#data-privacy)
* [Project Status](#project-status)

---

## ⚙️ Core Functionality

OTAP processes continuous video streams using CUDA-accelerated OCR. 

1. **Vision Pipeline:** Raw video is processed on an NVIDIA Tesla P4 GPU.
2. **Detection Logic:** The system evaluates every license plate against a recent history. 
3. **Event Creation:** If a plate has not been recorded within the last 10 minutes, a new event is generated.

### Event Schema
Each event is a discrete log entry consisting of:
* `Timestamp`: Accurate system time.
* `Plate Number`: The decoded alphanumeric string.
* `Latitude/Longitude`: Geographic data retrieved via the ESP32 sensor module.

---

## 🛡️ Design Philosophy

We prioritize privacy through strict, minimal-scope design:

* **Edge-Only Processing:** All detection, inference, and storage occur locally on the device hardware. No telemetry is sent off-device.
* **Minimal Scope:** The system is strictly limited to license plate recognition. It **does not** perform facial recognition, person identification, or behavioral inference.
* **Offline Independence:** OTAP functions fully offline once initialized.
* **Event-Based Logging:** We record discrete sightings rather than continuous tracking streams, keeping the dataset lightweight and manageable.

---

## 🛠️ Hardware Architecture

OTAP is engineered for in-vehicle deployment on x86-based embedded systems. 

| Component | Role |
| :--- | :--- |
| **Host System** | ITX Motherboard / Intel i7 CPU |
| **Vision Processor** | NVIDIA Tesla P4 (CUDA-accelerated) |
| **Sensor Interface** | ESP32 Module (GPS + Time sync over WiFi) |
| **Input** | Multi-camera system (Vehicle exterior) |

### Storage
All events are stored locally in a standardized log file format. We explicitly avoid databases, cloud services, or external synchronization to ensure the operator retains full control of the data.

---

## 🚀 Project Status
OTAP is currently in **early development**. 

* **Operational:** Core processing pipeline and hardware integration.
* **In Progress:** Ongoing refinement of detection accuracy and system stability.

---

*This project was developed as an alternative to modern, cloud-dependent dash camera systems.*
