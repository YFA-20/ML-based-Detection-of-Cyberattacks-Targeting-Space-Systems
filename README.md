# ML-based Detection of Cyberattacks Targeting Space Systems

This repository contains a machine learning project focused on detecting cyberattacks and anomalies targeting space systems.  
The idea is to use data from different layers of the space ecosystem:

- satellite telemetry,
- IoT/IIoT and cyber-physical devices,
- network traffic and system-level indicators (ground segment).

The long-term goal is to build and compare models that can perform both binary classification (attack vs. normal) and multi-class classification (attack types).

---

## Datasets

The project is designed around three public datasets, each covering a different aspect of the problem.

### 1. OPSSAT-AD: Satellite Telemetry Anomaly Detection

**Link:**  
https://www.kaggle.com/datasets/orvile/satellite-telemetry-data-anomaly-prediction  

This dataset is based on telemetry from the OPSSAT CubeSat mission operated by the European Space Agency.  
It provides:

- raw telemetry segments,
- and a tabular version with precomputed features (statistical and signal-based),
- with labels indicating nominal vs. anomalous behaviour.

This dataset represents the **space segment** (on-board telemetry).

---

### 2. TON_IoT: IoT / IIoT and Cyber-physical Systems

**Link:**  
https://research.unsw.edu.au/projects/toniot-datasets  

TON_IoT is a collection of datasets for IoT and Industrial IoT environments.  
It includes:

- telemetry from various IoT devices (sensors, actuators, smart home devices, etc.),
- network traffic captures,
- system and security event logs,
- labels for normal behaviour and different types of attacks.

This dataset is relevant for modelling the **ground and edge infrastructure** that can support space systems (e.g. control equipment, industrial interfaces, auxiliary sensors).

---

### 3. Network Intrusion Dataset (CIC-IDS 2017)

**Link:**  
https://www.kaggle.com/datasets/chethuhn/network-intrusion-dataset  

This dataset contains network flows labelled as normal or various attack categories.  
It is commonly used for intrusion detection research and includes features extracted from traffic captures (flows, bytes, packets, flags, etc.).

It represents the **network security aspect** of the ground segment (ground stations, mission control networks, support infrastructure).

---

## Project status

The repository will gradually include:

- data loading and preprocessing scripts or notebooks for each dataset,
- baseline machine learning models (e.g. Decision Trees, SVM, Random Forest),
- hyperparameter tuning,
- and evaluation using standard metrics (accuracy, precision, recall, F1-score, confusion matrices).

At this stage, the code and experiments are still under development and the structure of the project may evolve.
