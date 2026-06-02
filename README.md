<div align="center">

<img src="https://img.shields.io/badge/⚡-PROJECT%20AURORA-0ea5e9?style=for-the-badge&labelColor=0f172a&color=0ea5e9" alt="Project Aurora" height="40"/>

**Self-Learning Notification Orchestrator**

*Kriti 2026 · SpeakX Challenge · Hostel 2613 · IIT Guwahati*

<br/>

[![Demo](https://img.shields.io/badge/▶%20Watch%20Demo-Google%20Drive-4285F4?style=flat-square&logo=googledrive&logoColor=white)](https://drive.google.com/file/d/1c_yMBaIjrgGrG-4bzWlv0tDpM2K6HmWy/view?usp=drivesdk)
[![Repo](https://img.shields.io/badge/GitHub-basednucleophile%2FSpeakX__Aurora2613-181717?style=flat-square&logo=github)](https://github.com/basednucleophile/SpeakX_Aurora2613)
[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=flat-square&logo=python&logoColor=white)](https://python.org)
[![Gemini](https://img.shields.io/badge/Gemini-2.5%20Flash-8E75B2?style=flat-square&logo=google&logoColor=white)]()
[![Claude](https://img.shields.io/badge/Claude-Sonnet%204.6-D97757?style=flat-square)]()

<br/>

> Domain-agnostic, self-learning notification orchestration pipeline.  
> Ingests a company **Knowledge Bank** + **user behavioral CSV** → outputs personalized notification schedules that improve over time via reinforcement learning.  
> Built on SpeakX (AI English learning) · plug-and-play for any B2C or B2B product by swapping the KB and dataset.

</div>

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                                                                         │
│   company_kb.md ──┐                                                     │
│                   ├──▶  TASK 1  ──▶  TASK 2  ──▶  TASK 3  ──▶  OUTPUT  │
│   user_data.csv ──┘                    ▲                                │
│                                        │                                │
│   experiment_results.csv ─────────────┘  (Demo 2 feedback loop)        │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## Pipeline

<details open>
<summary><strong>Task 1 — System Architecture &amp; Intelligence Design</strong></summary>
<br/>

| Component | Details |
|:---|:---|
| **Knowledge Bank Engine** `Gemini 2.5 Flash` | Extracts north star metric, feature-goal mappings, tone/hook matrix, propensity dimensions, journey/goal templates from any company KB |
| **User Data Ingestion** | 5-layer validation pipeline: schema → types → ranges → imputation → dedup on behavioral CSV |
| **MECE Segmentation Engine** | K-Means on KB-derived propensity space (`gamification`, `ai_tutor`, `leaderboard`, `social`); silhouette sweep k=6–12; within-lifecycle percentile normalization; 3-axis persona naming (dominant × activeness × churn) with iterative collision resolution |
| **Goal & Journey Builder** | Generates primary goals, sub-goals, and day-on-day progression per Segment × Lifecycle from KB templates |

</details>

<details open>
<summary><strong>Task 2 — Communication &amp; Timing Intelligence</strong></summary>
<br/>

| Component | Details |
|:---|:---|
| **Theme Engine** `Gemini` | Maps top-3 Octalysis drives per segment |
| **Template Generator** `Gemini REST` | 5 bilingual templates per Segment × Lifecycle × Theme (English + Hinglish); concurrent batched generation |
| **Timing Optimizer** | 4-model comparison (RF · GB · LR · SVM) on `preferred_hour → time_zone` classification; outputs top-3 zones per user and per segment |
| **Schedule Generator** `Claude Sonnet 4.6` | Octalysis drive scoring; activeness-based frequency (3–9/day); zone-aware channel routing (`push` / `in_app` / `whatsapp` / `sms`); template-to-notification mapping |

</details>

<details open>
<summary><strong>Task 3 — Execution &amp; Self-Learning</strong></summary>
<br/>

| Component | Details |
|:---|:---|
| **RL Classification** | Grid-search optimal reward weights (CTR · engagement · uninstall penalty); Bayesian engagement estimation; quantile-based GOOD / NEUTRAL / BAD classification with confidence gating |
| **Strategy Generator** | Traffic allocation — GOOD `70%` · NEUTRAL `25%` · BAD `5%`; segment safety analysis (uninstall guardrails); optimal timing analysis |
| **Goal Updater** `Gemini` | 3-tier strategy: GOOD preserved · NEUTRAL gets A/B variants · BAD rewritten; causal reasoning from RL data |
| **Iteration 1 Generator** | Regenerates only changed templates; RL-informed template scoring; guardrail frequency reduction for high-uninstall segments |
| **Delta Report** | Every change documented with causal explanation |

</details>

---

## Models

| Model | Provider | Role |
|:---|:---|:---|
| `gemini-2.5-flash` | Google GenAI | KB extraction · theme mapping · goal optimization · template generation |
| `claude-sonnet-4-6` | Anthropic | Octalysis drive scoring for schedule generation |
| RF · GB · LR · SVM | scikit-learn | K-Means segmentation · notification timing classification |

---

## Results

<details open>
<summary><strong>Timing Model Comparison</strong></summary>
<br/>

| Model | Accuracy | F1 Score | Cross-Val |
|:---|:---:|:---:|:---:|
| Random Forest | 0.2733 | 0.1842 | 0.2580 |
| Gradient Boosting | 0.2300 | 0.1674 | 0.2467 |
| Logistic Regression | 0.2700 | 0.1474 | 0.3033 |
| **SVM (RBF)** ✓ | **0.2767** | **0.1953** | 0.2553 |

</details>

<details open>
<summary><strong>Best Notification Windows</strong></summary>
<br/>

| Rank | Zone | Window | Avg. Engagement |
|:---:|:---|:---|:---:|
| 🥇 | Evening | 18:00 – 20:59 | `0.72` |
| 🥈 | Night | 21:00 – 23:59 | `0.58` |
| 🥉 | Early Morning | 06:00 – 08:59 | `0.61` |
| — | Mid Morning | 09:00 – 11:59 | `0.55` |
| — | Afternoon | 12:00 – 14:59 | `0.43` |
| — | Late Afternoon | 15:00 – 17:59 | `0.39` |

</details>

---

## Setup

**Install dependencies:**
```bash
pip install -r requirements.txt
```

**Required input files** (place in working directory):

| File | Description |
|:---|:---|
| `user_behavioral_data.csv` | 1500 users — schema per PS |
| `company_kb.md` | Company knowledge bank |
| `experiment_results.csv` | Provided by SpeakX for Demo 2 |

> ✅ Windows compatible — all paths use `os.path.join`, no Unix-specific commands.

---

## Run

**Full pipeline:**
```bash
python codebase/run_pipeline.py \
  --data user_behavioral_data.csv \
  --kb company_kb.md \
  --experiment experiment_results.csv
```

**Trial run:**
```bash
python codebase/run-trial.py
```

<details>
<summary><strong>Run step by step</strong></summary>
<br/>

```bash
# Task 1 — Intelligence & Segmentation
python codebase/task1_aurora.py

# Task 2 — Communication & Timing
python codebase/theme_engine.py
python codebase/generate_templates.py
python codebase/timing_optimizer.py
python codebase/schedule_generator.py

# Task 3 — Self-Learning Loop
python codebase/task3_learning_engine.py
python codebase/generate_delta_report.py
```

</details>

---

## Structure

```
SpeakX_Aurora2613/
│
├── codebase/
│   ├── task1_aurora.py              ← KB extraction + segmentation
│   ├── theme_engine.py              ← Octalysis theme mapping
│   ├── generate_templates.py        ← Bilingual template generation
│   ├── timing_optimizer.py          ← ML timing prediction
│   ├── schedule_generator.py        ← Schedule + channel routing
│   ├── task3_learning_engine.py     ← RL classification + strategy
│   ├── generate_delta_report.py     ← Delta report generation
│   ├── run_pipeline.py              ← Full pipeline entrypoint
│   └── run-trial.py                 ← Trial run script
│
├── iteration_0_before_learning/     ← Outputs pre-RL
├── iteration_1_after_learning/      ← Outputs post-RL
├── _internal_debug/
├── requirements.txt
└── README.txt
```

---

<div align="center">
<sub>Kriti 2026 · IIT Guwahati · Hostel 2613</sub>
</div>
