# Early-Warning Rule Mining for Turbofan Engine Degradation

## Abstract

**Dataset Chosen**  
Real — [NASA C-MAPSS Turbofan Degradation Simulation](https://www.kaggle.com/datasets/behrad3d/nasa-cmaps?phase=FinishSSORegistration&returnUrl=%2Fdatasets%2Fbehrad3d%2Fnasa-cmaps%2Fversions%2F1%3Fresource%3Ddownload&SSORegistrationToken=CfDJ8HYJ4SW6YXhJj8CRciRldeQp3vLwXO6nzSOXQNl5WM8uj81ufxise7BG1lIuAdtFOhJ3kZQmvZPY-UZRBleTT4Ms8tMW82ia1BQ0goXwMrf9Xxpyt6OwSTRptS-C6S9R8lU1g0aeDNQQEx3UnanEx371bU4zxHOtVoJ3sbPDiIwBWuEwLPjo45t3wpxb-BFrcfIbBGW0kj40tW1aD2dIeq5hibfSw3BfJt2k8109UXTuOy4oPzK3kCVXhtMc1WIH28b0mVG8WZBf0goflvAcB8NfaVsKqZupO47ML2KG9QhegtFMVY2BAZ3QXR0HYdmOO4qWrro2Vntj_JnZZZE6IZl4C4A0&DisplayName=Nut%27+ella), subset FD001 (100 engines, 21 sensors)

**Goal**  
This study investigates whether interpretable association rules can serve as reliable early-warning indicators for jet-engine failure. We ask: *Which combinations of sensor behaviours systematically precede a drop in remaining useful life (RUL) below 50 cycles?*

**Features of Interest**  
Time-series readings from 21 on-board sensors (temperatures, pressures, fan speed, fuel-flow, vibration) plus three operating-condition variables.

**Plan to Handle Continuous Variables**  
For each sliding window of 25 cycles we:  
1. Discretise sensor values into **Low** (≤10th percentile), **Normal**, **High** (≥90th percentile).  
2. Label short-term trends as **Rising** or **Falling** via first-difference sign.  
3. Encode each window as a transaction containing the active categorical flags.

**Proposed Rule-Mining Approach**  
FP-Growth with *min-support* = 3 % and *min-confidence* = 0.8, followed by filtering on lift > 1.5. Consequents are restricted to the binary target *Fail ≤ 50*.

**Expected Outcome**  
We expect to discover a concise set of high-lift rules (e.g., `{T50_High, s11_Rising, s15_Drop} → Fail ≤ 50`) that predict imminent failure with ≥80 % confidence and offer >1.5× information gain over baseline.

**Why This Matters**  
The resulting rule set provides a transparent decision layer for airline maintenance and MRO teams. By flagging hazardous sensor patterns up to 50 cycles in advance, operators can schedule inspections, prevent in-service shutdowns, and cut unplanned downtime—while retaining full interpretability for engineering audit and regulatory compliance.
