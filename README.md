# ML-based Detection of Cyberattacks Targeting Space Systems

This repository contains a machine learning project focused on detecting cyberattacks and anomalies targeting space systems.

The project relies on data originating from multiple layers of the space ecosystem:

- **Satellite telemetry** (space segment)
- **IoT / IIoT and cyber-physical devices** (ground segment – OT)
- **Network traffic and system-level indicators** (ground segment – IT)

The objective is to train specialized detection models for each layer and to combine their outputs inside a **centralized Mission Control fusion engine**, capable of correlating isolated alerts into a global threat assessment.

The system supports both **binary classification** (normal vs. attack) and **multi-class classification** (attack types), with a focus on coordinated and multi-vector attack scenarios.

---

## Repository Structure

The project is organized to ensure traceability from raw datasets to trained models and final fusion logic.

```text
├── datasets/               # Raw data sources (compressed as .zip archives)
├── mission_control/        # [MAIN] Fusion engine and simulation logic
│   └── Mission_Control_Fusion.ipynb
├── models/                 # Pre-trained and serialized model artifacts
│   ├── model_satellite.pkl     # Voting Classifier (telemetry)
│   ├── model_industrial.json   # XGBoost (JSON serialization)
│   ├── model_network.pkl       # Stacking Classifier (network traffic)
│   └── scaler_network.pkl      # Feature scaling for network data
├── notebooks_training/     # Training and export notebooks
│   ├── 01_Train_Satellite_Final.ipynb
│   ├── 02_Train_Industrial_Final.ipynb
│   └── 03_Train_Network_Final.ipynb
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
```
## Data Handling Note

Due to GitHub’s **100 MB per-file limit**, all raw CSV datasets are stored as **ZIP archives** in the `datasets/` directory.

The training notebooks are configured to read compressed datasets directly.

If manual inspection or external tooling is used, the archives must be extracted beforehand.

---

## Datasets

The project relies on three public datasets, each covering a different layer of the attack surface.

### OPSSAT-AD – Satellite Telemetry Anomaly Detection

**Link:**  
https://www.kaggle.com/datasets/orvile/satellite-telemetry-data-anomaly-prediction

This dataset is based on telemetry from the OPSSAT CubeSat mission operated by the European Space Agency.

It provides:

- raw telemetry segments
- precomputed statistical and signal-based features
- labels indicating nominal versus anomalous behaviour

This dataset represents the **space segment**, focusing on on-board telemetry integrity.

---

### TON_IoT – IoT / IIoT and Cyber-physical Systems

**Link:**  
https://research.unsw.edu.au/projects/toniot-datasets

TON_IoT is a heterogeneous dataset collection targeting IoT and Industrial IoT environments.

It includes:

- telemetry from sensors, actuators, and cyber-physical devices
- network traffic captures
- system and security event logs
- labels for normal behaviour and multiple attack types

This dataset models the **ground and edge infrastructure** that supports space systems.

---

### CIC-IDS 2017 – Network Intrusion Detection

**Link:**  
https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset

This dataset contains labelled network flows for intrusion detection research.

It includes features extracted from traffic captures such as flow statistics, packet counts, byte volumes, and protocol flags.

It represents the **network security layer** of the ground segment.

---

## Project Status

The repository implements a functional end-to-end detection and fusion pipeline.

### Detection Models

- **Space segment:** Voting Classifier for satellite telemetry status
- **Industrial segment:** XGBoost classifier, serialized in JSON for portability and version safety
- **Network segment:** Stacking Classifier for flow-based intrusion detection

---

### Mission Control and Fusion Logic

A centralized fusion engine located in `mission_control/` aggregates predictions from the three specialized models.

A **late-fusion strategy** is used to correlate independent alerts into a unified threat level, enabling detection of coordinated attacks such as network intrusions combined with industrial sabotage.

---

### Validation and Simulation

The `Mission_Control_Fusion.ipynb` notebook includes a simulation loop validating the system against multiple scenarios:

- nominal operation
- isolated satellite anomaly
- isolated network attack
- coordinated ground attack triggering a **critical alert level (Level 5)**

---

## Quick Start

1. Clone the repository  
2. Install dependencies using:
   ```bash
   pip install -r requirements.txt

4. Open `mission_control/Mission_Control_Fusion.ipynb` and execute all cells

---

## Technical Notes

- GitHub enforces a strict **100 MB per-file limit**, justifying dataset compression
- XGBoost JSON serialization is used for version-safe model persistence
- The documented repository structure matches the actual project layout
- Critical fusion logic is validated by simulation logs indicating a **Level 5 ground compromise**

