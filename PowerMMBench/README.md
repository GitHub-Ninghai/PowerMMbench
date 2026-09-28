# PowerMMBench Dataset

PowerMMBench is a multimodal benchmark of **396 questions** for evaluating large language models in the power & energy domain. It spans 4 major categories and 29 sub-categories, covering text, image, time-series and video modalities.

## Directory structure

```
PowerMMBench/
├── demand_side/   # 62 questions
│   ├── demand_response/  [1 q]  (images/)
│   ├── distributed_energy/  [4 q]  (images/)
│   ├── ev_charging/  [25 q]  (images/)
│   ├── load_forecasting/  [18 q]  (images/)
│   ├── user_behavior/  [12 q]  (images/)
│   ├── virtual_power_plant/  [2 q]  (images/)
├── market_policy/   # 27 questions
│   ├── ancillary_service/  [9 q]
│   ├── carbon_green/  [1 q]  (images/)
│   ├── midlong_term/  [1 q]  (images/)
│   ├── policy_regulation/  [10 q]  (images/)
│   ├── pricing_tariff/  [5 q]  (images/)
│   ├── spot_market/  [1 q]
├── power_equipment/   # 157 questions
│   ├── cable/  [5 q]  (images/)
│   ├── insulation/  [16 q]  (images/)
│   ├── meter_reading/  [7 q]  (images/)
│   ├── partial_discharge/  [15 q]  (images/)
│   ├── power_electronics/  [40 q]  (images/)
│   ├── rotating_machine/  [20 q]  (images/)
│   ├── switchgear/  [9 q]  (images/)
│   ├── thermal_imaging/  [12 q]  (images/)
│   ├── transformer/  [9 q]  (images/)
│   ├── visual_inspection/  [24 q]  (videos/)
├── power_grid/   # 150 questions
│   ├── dispatch_operation/  [47 q]  (images/)
│   ├── fault_diagnosis/  [8 q]  (images/)
│   ├── grid_topology/  [19 q]  (images/)
│   ├── power_flow/  [17 q]  (images/)
│   ├── relay_protection/  [17 q]  (images/)
│   ├── stability_analysis/  [12 q]  (images/)
│   ├── transmission_line/  [30 q]  (images/)
│       ├── questions.jsonl
│       ├── images/       # images referenced by the questions
│       └── videos/       # videos referenced by the questions (visual_inspection only)
└── questions_final.json  # flat copy of all 396 questions
```

Each `questions.jsonl` line is one question record with fields: `id`, `source`, `question_type`, `domain`, `difficulty`, `question`, `options`, `answer`, `explanation`, `has_image`, `images`, `has_video`, `videos`, `metadata`, `major_category`, `minor_category`.

## Statistics

| Major category | Sub-category | Questions | Type breakdown | Difficulty |
|---|---|---|---|---|
| **demand_side** | demand_response | 1 | multiple_choice 1 | hard 1 |
|  | distributed_energy | 4 | multiple_choice 3, text_qa 1 | medium 2, hard 2 |
|  | ev_charging | 25 | multiple_choice 25 | hard 25 |
|  | load_forecasting | 18 | multiple_choice 18 | hard 16, medium 2 |
|  | user_behavior | 12 | multiple_choice 12 | hard 11, medium 1 |
|  | virtual_power_plant | 2 | multiple_choice 2 | hard 2 |
| **market_policy** | ancillary_service | 9 | multiple_choice 9 | hard 9 |
|  | carbon_green | 1 | multiple_choice 1 | hard 1 |
|  | midlong_term | 1 | multiple_choice 1 | hard 1 |
|  | policy_regulation | 10 | multiple_choice 8, text_qa 2 | medium 10 |
|  | pricing_tariff | 5 | multiple_choice 2, text_qa 2, subjective 1 | medium 5 |
|  | spot_market | 1 | text_qa 1 | medium 1 |
| **power_equipment** | cable | 5 | multiple_choice 5 | medium 5 |
|  | insulation | 16 | multiple_choice 16 | medium 15, hard 1 |
|  | meter_reading | 7 | multiple_choice 7 | medium 7 |
|  | partial_discharge | 15 | multiple_choice 15 | hard 15 |
|  | power_electronics | 40 | multiple_choice 40 | medium 39, hard 1 |
|  | rotating_machine | 20 | multiple_choice 20 | medium 20 |
|  | switchgear | 9 | multiple_choice 8, subjective 1 | medium 9 |
|  | thermal_imaging | 12 | multiple_choice 12 | hard 12 |
|  | transformer | 9 | multiple_choice 9 | medium 9 |
|  | visual_inspection | 24 | subjective 24 | easy 12, hard 12 |
| **power_grid** | dispatch_operation | 47 | multiple_choice 22, text_qa 21, time_series_analysis 3, subjective 1 | medium 44, hard 2, easy 1 |
|  | fault_diagnosis | 8 | multiple_choice 8 | medium 8 |
|  | grid_topology | 19 | multiple_choice 19 | medium 19 |
|  | power_flow | 17 | multiple_choice 10, time_series_analysis 6, text_qa 1 | medium 13, very_hard 3, easy 1 |
|  | relay_protection | 17 | multiple_choice 10, text_qa 7 | medium 17 |
|  | stability_analysis | 12 | multiple_choice 8, time_series_analysis 3, text_qa 1 | medium 8, hard 3, easy 1 |
|  | transmission_line | 30 | multiple_choice 26, time_series_analysis 3, text_qa 1 | medium 29, hard 1 |

**Totals**: 396 questions — types: multiple_choice 317, text_qa 37, subjective 27, time_series_analysis 15; difficulty: medium 263, hard 115, easy 15, very_hard 3; 309 images; 12 videos (24 video questions).

## Sources

Questions are derived from registered electrical engineer exam archives, industry standards, PowerMMBench collection pipelines and the [ElecBench](../Elecbench) / [MMEBench](../MMEBench) data families. Per-question provenance is kept in the `metadata` and `source` fields.
