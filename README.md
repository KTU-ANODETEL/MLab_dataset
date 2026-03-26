# ANODOTEL Part 1 Dataset No: 1 - Experimental Power Event Measurements

> Experimental smart meter measurement dataset collected in a real university office building environment, preprocessed for power event detection and machine learning research.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Status: Public](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow)]()
[![Funded by LMTLT](https://img.shields.io/badge/Funded%20by-LMTLT%20S--MIP--24--42-orange)]()

---
 
## Overview
 
This repository contains a comprehensive dataset of experimental measurement results. The experiments were conducted in a **university office building** equipped with typical office infrastructure, including personal computers, large display screens, electrical kettles, etc.
 
Both the **sum meter** and the **consumer meter** were connected to the same single-phase branch on the same floor of the building. Both meters are **Class I**, transmitting data via the **P1 port** at **1-second intervals**. The transmitted data package complies with the **Dutch Smart Meter Requirements DSMR 5.0**.
 
In order to select power events more precisely, preprocessing was performed on the experimental data according to the following criteria:
 
- **`tm`** — number of samples used for mean power consumption calculation before and after a power event
- **`dev`** — standard deviation threshold [W] of power consumption samples in the range before and after the power event edge
 
---
 
## Dataset Structure
 
The repository contains two types of data: **raw meter recordings** (continuous time-series from P1 smart meter interface) and **preprocessed event files** (extracted power events in XLSX format).
 
---
 
## Raw Data
 
Raw recordings are provided as CSV files captured directly from the P1 smart meter interface at ~1 second sampling interval.

---

### Raw Data Columns
 
Each row represents one meter reading. Two meters (sum and consumer) report alternately via a single reporter device, identified by `equipment_identifier`.
 
> **Single-phase data only.** Although the P1 interface provides fields for three phases (L1, L2, L3), only **L1 data is populated** in this dataset. All L2 and L3 columns are `NaN`.
 
| Column | Unit | Description |
|--------|------|-------------|
| `ntp_time` | — | Timestamp of the reading (NTP-synchronized, ~1 s interval) |
| `equipment_identifier` | — | Unique meter ID (sum meter or consumer meter) |
| `reporter_device` | — | MAC address of the P1 interface reporting device |
| `active_energy_export` | Wh | Cumulative active energy exported to grid |
| `active_energy_import` | Wh | Cumulative active energy imported from grid |
| `instantaneous_active_export_power_l1` | W | Instantaneous active export power, phase L1 |
| `instantaneous_active_import_power_l1` | W | Instantaneous active import power, phase L1 |
| `instantaneous_active_import_power_l2` | W | Instantaneous active import power, phase L2 |
| `instantaneous_active_import_power_l3` | W | Instantaneous active import power, phase L3 |
| `instantaneous_current_l1` | A | Instantaneous current, phase L1 |
| `instantaneous_current_l2` | A | Instantaneous current, phase L2 |
| `instantaneous_current_l3` | A | Instantaneous current, phase L3 |
| `instantaneous_power_factor_l1` | — | Power factor, phase L1 |
| `instantaneous_power_factor_l2` | — | Power factor, phase L2 |
| `instantaneous_power_factor_l3` | — | Power factor, phase L3 |
| `instantaneous_reactive_export_power_l1` | Var | Instantaneous reactive export power (inductive), phase L1 |
| `instantaneous_reactive_export_power_l2` | Var | Instantaneous reactive export power (inductive), phase L2 |
| `instantaneous_reactive_export_power_l3` | Var | Instantaneous reactive export power (inductive), phase L3 |
| `instantaneous_reactive_import_power_l1` | Var | Instantaneous reactive import power (capacitive), phase L1 |
| `instantaneous_reactive_import_power_l2` | Var | Instantaneous reactive import power (capacitive), phase L2 |
| `instantaneous_reactive_import_power_l3` | Var | Instantaneous reactive import power (capacitive), phase L3 |
| `instantaneous_voltage_l1` | V | Instantaneous voltage, phase L1 |
| `instantaneous_voltage_l2` | V | Instantaneous voltage, phase L2 |
| `instantaneous_voltage_l3` | V | Instantaneous voltage, phase L3 |
| `total_harmonic_distortion_l1` | % | Total harmonic distortion, phase L1 |
| `total_harmonic_distortion_l2` | % | Total harmonic distortion, phase L2 |
| `total_harmonic_distortion_l3` | % | Total harmonic distortion, phase L3 |
| `valid_crc` | — | CRC validity flag (1 = valid, 0 = invalid) |
  
---

## Preprocessed Event Files
 
Files are organized by **sample window** (`tm`) and **deviation threshold** (`dev`):

### File Naming Convention

```
MLab_dataset_no1_tm{N}_dev{D}.xlsx
```

| Token | Meaning | Values |
|-------|---------|--------|
| `tm{N}` | Number of samples for mean power calculation before/after event | 1 – 10 |
| `dev{D}` | Standard deviation threshold of samples near event edge [W] | 10, 30 |

### File Tree

```
📦 MLab_Dataset_No1
 ┣ 📊 MLab_dataset_no1_tm1_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm2_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm3_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm4_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm5_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm6_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm7_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm8_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm9_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm10_dev10.xlsx
 ┣ 📊 MLab_dataset_no1_tm1_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm2_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm3_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm4_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm5_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm6_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm7_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm8_dev30.xlsx
 ┣ 📊 MLab_dataset_no1_tm9_dev30.xlsx
 ┗ 📊 MLab_dataset_no1_tm10_dev30.xlsx
```

> **20 files total** — 10 values of `tm` × 2 values of `dev`.

### Event Count vs. Preprocessing Parameters


---

## Data Columns

Each file contains **20 columns** with before/after snapshots of electrical quantities at the moment of a power event:

### Active Power

| Column | Unit | Description |
|--------|------|-------------|
| `Ps1` | W | Active power of sum meter **before** power event |
| `Ps2` | W | Active power of sum meter **after** power event |
| `Pc1` | W | Active power of consumer meter **before** power event |
| `Pc2` | W | Active power of consumer meter **after** power event |

### Current

| Column | Unit | Description |
|--------|------|-------------|
| `Is1` | A | Current of sum meter **before** power event |
| `Is2` | A | Current of sum meter **after** power event |
| `Ic1` | A | Current of consumer meter **before** power event |
| `Ic2` | A | Current of consumer meter **after** power event |

### Voltage

| Column | Unit | Description |
|--------|------|-------------|
| `Vs1` | V | Voltage of sum meter **before** power event |
| `Vs2` | V | Voltage of sum meter **after** power event |
| `Vc1` | V | Voltage of consumer meter **before** power event |
| `Vc2` | V | Voltage of consumer meter **after** power event |

### Reactive Power

| Column | Unit | Description |
|--------|------|-------------|
| `Qps1` | Var | Reactive import power (inductive), sum meter, **before** power event |
| `Qps2` | Var | Reactive import power (inductive), sum meter, **after** power event |
| `Qns1` | Var | Reactive export power (capacitive), sum meter, **before** power event |
| `Qns2` | Var | Reactive export power (capacitive), sum meter, **after** power event |
| `Qpc1` | Var | Reactive import power (inductive), consumer meter, **before** power event |
| `Qpc2` | Var | Reactive import power (inductive), consumer meter, **after** power event |
| `Qnc1` | Var | Reactive export power (capacitive), consumer meter, **before** power event |
| `Qnc2` | Var | Reactive export power (capacitive), consumer meter, **after** power event |

---

## Preprocessing Parameters Explained

| Parameter | Description |
|-----------|-------------|
| `tm` | Number of samples averaged on each side of the event edge to compute stable before/after values. Higher `tm` → smoother mean, fewer edge effects. |
| `dev` | Maximum allowed standard deviation [W] of samples in the window before/after the event edge. Lower `dev` → only clean, stable transitions are kept. |

**Available configurations:**

| `dev` \ `tm` | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **10 W** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **30 W** | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |

---

## Applications

This dataset is suitable for:

- 🔌 **Smart Meter Research** — real-world validation of meter error detection and power event detection methods
- 🤖 **Machine Learning** — training and benchmarking classifiers for power event recognition
- 📊 **Algorithm Testing** — evaluating sensitivity of preprocessing parameters (`tm`, `dev`) on detection quality
- 🎓 **Education** — demonstration of real power event characteristics in single-phase low-voltage networks

---

## License

This dataset is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

You are free to share and adapt the data for any purpose, including commercial use, provided appropriate credit is given to the authors and the source publication is cited.

---

## Related Publications

> Šaltanis, J., Saunoris, M., Lukočius, R., Daunoras, V., Zulonas, K., Rinaldi, S., & Nakutis, Ž. **" TBW "** 

---

## Acknowledgments

This research was funded by the **Research Council of Lithuania (LMTLT)**, grant number **S-MIP-24-42**.

**Institution:** Faculty of Electrical and Electronics Engineering, Kaunas University of Technology

---

## Authors & Contributors

**¹ Faculty of Electrical and Electronics Engineering, Kaunas University of Technology:**

| Name | Email |
|------|-------|
| Julius Šaltanis | julius.saltanis@ktu.lt |
| Marius Saunoris | marius.saunoris@ktu.lt |
| Robertas Lukočius | robertas.lukocius@ktu.lt |
| Vytautas Daunoras | vytautas.daunoras@ktu.lt |
| Kasparas Zulonas | kasparas.zulonas@ktu.lt |
| **Žilvinas Nakutis** ⭐ | zilvinas.nakutis@ktu.lt |

**² Department of Information and Industrial Engineering, University of Brescia, Italy:**

| Name | Email |
|------|-------|
| Stefano Rinaldi | stefano.rinaldi@unibs.it |

⭐ *Corresponding authors*

**Institution:** Kaunas University of Technology, LT-51368 Kaunas, Lithuania

## Contact

For questions or collaboration inquiries, please [open a GitHub issue](../../issues).

**Project:** KTU-ANODETEL  
**Institution:** Kaunas University of Technology  
**Department:** Electronics Engineering

---

**Keywords:** `smart metering` `power events` `anomaly detection` `experimental dataset` `low voltage` `single phase` `office building` `machine learning` `energy monitoring`
