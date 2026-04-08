# QDET:Query-Driven Event Timeline Summarization
This repository contains the sample dataset and supporting materials for the paper **QDET: Query-Driven Event Timeline Summarization for Industrial Search Engines**, which corresponds to the deployed production system on Baidu Search.

## Overview
Understanding event evolution is critical for search engines processing trending news queries. We present**QDET (Query-Driven Event Timeline Summarization)**, a production system on Baidu Search that constructs focused timelines to explain specific query events. Unlike traditional topic-centric approaches pursuing comprehensive coverage, QDET identifies and organizes query-relevant sub-events from noisy daily document candidates.

## Key Innovations

1. **Multi-task Supervised Fine-tuning**
Three auxiliary tasks (temporal ordering, causal judgment, timeline completion) enable compact models to match larger general-purpose models in timeline domains.

2. **Reinforcement Learning-based Concise Summarization**
RL enforces strict length constraints (5–15 Chinese characters) while preserving semantics, achieving 88.2% length compliance and outperforming 671B-scale models by 7.7 points in constraint satisfaction.

3. **Efficient Small Model Design**
Our 7B fine-tuned model achieves 76.2% F1 (timeline summarization), slightly surpassing DeepSeek-R1-671B (76.1% F1, zero-shot) with only 1% of its parameters, enabling low-cost industrial deployment.

4. **Real-world Industrial Effectiveness**
Online A/B tests on Baidu Search show: 5.5% CTR improvement, 4.6% longer dwell time, 4.4% deeper exploration. Timeline understanding also transfers effectively to downstream heat prediction.


## Dataset Release Plan

Due to **strict Baidu open-source review policies and data security & ownership regulations**, we adopt a phased data release strategy:

### Current Release (v1.0)

We publicly release **100 real query-driven event timeline samples** from our actual training corpus.
- Consistent with real training data format.
- Format: One JSON object per line (includes `query-driven`, `event_list`, `event_num`,`hot_level`, etc.).
- Purpose: Help readers understand data construction, event chain design, and summarization logic.

### Future Release (Expected August 2026)

If internal review proceeds smoothly, we will release:
1. Full training dataset (8,000 human-annotated query-driven timelines)
2. Complete QDET training/inference code
3. Evaluation scripts and baseline implementation

## Dataset Structure

The 100 sample data is stored in:

```plain text
data/
├── qdet_timeline_samples_100.jsonl  # 100 query-driven timeline samples (Chinese, one JSON per line)
└── qdet_timeline_samples_100_en.jsonl  # 100 query-driven timeline samples (English, one JSON per line)
```


### Data Field Description

- `query-driven`: Query-centric event name (reconstructed from the timeline's final event, e.g., "小米YU7路试图曝光引网友热议")

- `event_list`: Chronological event chain, each event includes:
                  -`event_name`: Concise event summary (5–15 Chinese characters, e.g., "网友偶遇雷军测试小米SUV车型")
                  - `event_time`: Event occurrence time (e.g., "2024-11-22 16:32:21")
                  - `event_url`: Original news source link
                  - `heat_label`: Event heat label (value: 1-5, indicating different heat levels, 5 represents the highest heat)

- `event_num`: Total number of events in the timeline (e.g., 6 in the sample JSON)


## Code & Usage

Currently, only the sample dataset is provided. Full training/inference code, configuration files, and evaluation pipelines will be open-sourced with the full dataset in August 2026.


