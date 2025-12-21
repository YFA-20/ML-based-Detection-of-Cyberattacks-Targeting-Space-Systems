```markdown
# ML-based Detection of Cyberattacks Targeting Space Systems

This repository contains a machine learning project focused on detecting cyberattacks and anomalies targeting space systems.
The idea is to use data from different layers of the space ecosystem:
* **Satellite telemetry** (Space segment).
* **IoT/IIoT and cyber-physical devices** (Ground segment - OT).
* **Network traffic and system-level indicators** (Ground segment - IT).

The long-term goal is to build and compare models that can perform both binary classification (attack vs. normal) and multi-class classification (attack types), culminating in a **Centralized Mission Control Engine** capable of multi-modal data fusion.

---

## Repository Structure

The project is organized to ensure full traceability from raw data to the final fusion engine.

```text
├── datasets/               # Raw data sources (Compressed as .zip archives)
├── mission_control/        # [MAIN] The Fusion Engine & Simulation Logic
│   └── Mission_Control_Fusion.ipynb
├── models/                 # Pre-trained & Serialized Model Artifacts
│   ├── model_satellite.pkl   (Voting Classifier)
│   ├── model_industrial.json (XGBoost in JSON for compatibility)
│   ├── model_network.pkl     (Stacking Classifier)
│   └── scaler_network.pkl    (Feature scaling for network data)
├── notebooks_training/     # Source code used to train and export the models
│   ├── 01_Train_Satellite_Final.ipynb
│   ├── 02_Train_Industrial_Final.ipynb
│   └── 03_Train_Network_Final.ipynb
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation

```

### Important Note on Data

Due to GitHub's file size limitations, the raw CSV files in the `datasets/` folder have been **compressed as ZIP archives**. The training notebooks are configured to handle this, but please ensure you unzip them if using external tools for manual analysis.

---

## Datasets

The project is designed around three public datasets, each covering a different aspect of the problem.

### 1. OPSSAT-AD: Satellite Telemetry Anomaly Detection

**Link:** https://www.kaggle.com/datasets/orvile/satellite-telemetry-data-anomaly-prediction

This dataset is based on telemetry from the OPSSAT CubeSat mission operated by the European Space Agency. It provides:

* Raw telemetry segments.
* A tabular version with precomputed features (statistical and signal-based).
* Labels indicating nominal vs. anomalous behaviour.

*This dataset represents the **space segment** (on-board telemetry).*

### 2. TON_IoT: IoT / IIoT and Cyber-physical Systems

**Link:** https://research.unsw.edu.au/projects/toniot-datasets

TON_IoT is a collection of datasets for IoT and Industrial IoT environments. It includes:

* Telemetry from various IoT devices (sensors, actuators, smart home devices, etc.).
* Network traffic captures.
* System and security event logs.
* Labels for normal behaviour and different types of attacks.

*This dataset is relevant for modelling the **ground and edge infrastructure** that can support space systems (e.g. control equipment, industrial interfaces, auxiliary sensors).*

### 3. Network Intrusion Dataset (CIC-IDS 2017)

**Link:** https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset

This dataset contains network flows labelled as normal or various attack categories. It is commonly used for intrusion detection research and includes features extracted from traffic captures (flows, bytes, packets, flags, etc.).

*It represents the **network security aspect** of the ground segment (ground stations, mission control networks, support infrastructure).*

---

## Project Status

The repository now implements a functional end-to-end detection and fusion pipeline:

1. **Model Implementation:**
* **Space Segment:** Ensemble model (Voting Classifier) for telemetry status.
* **Industrial Segment:** XGBoost Classifier optimized for hardware registers (serialized in JSON for cross-platform portability).
* **Network Segment:** Stacking Classifier for traffic flow analysis.


2. **Mission Control (Fusion Engine):**
A centralized module located in `mission_control/` that aggregates predictions from the three specialist models. It implements a **Late Fusion** logic to correlate isolated alerts into a global threat level. This allows for the detection of coordinated attacks, such as a network intrusion combined with industrial sabotage.
3. **Validation & Simulation:**
The `Mission_Control_Fusion.ipynb` notebook includes a simulation loop to validate the system against four specific scenarios: *Nominal*, *Satellite Anomaly*, *Network Attack*, and *Coordinated Ground Attack (Critical Level 5)*.

---

## Quick Start

To run the fusion simulation:

1. Clone the repository.
2. Install dependencies: `pip install -r requirements.txt`.
3. Open `mission_control/Mission_Control_Fusion.ipynb` and execute all cells.

```
