# PowerMMBench

**PowerMMBench** is a multimodal benchmark for evaluating large language models (LLMs / VLMs) in the power & energy domain, with **396 questions** across 4 major categories (power equipment, power grid, demand side, market & policy), 29 sub-categories, and four modalities (text, image, time series, video).

## Repository layout

| Path | Content |
|---|---|
| `index.html` → `benchmark_viewer.html` | Interactive question browser (same as the PowerMMBench website) |
| `questions_final.json` | Flat copy of all 396 questions |
| `power_equipment/` `power_grid/` `demand_side/` `market_policy/` | The dataset, nested by major category / sub-category |
| [`raw_data/Elecbench/`](raw_data/Elecbench) | Raw data of **ElecBench** (IEEE PESGM 2025 Best Paper), a power-dispatch evaluation benchmark: 4 test sets (general / monitoring / dispatch / blackstart), 288 questions |
| [`raw_data/MMEBench/`](raw_data/MMEBench) | MMEBench annotations and power-electronics industry images |

Each sub-category folder contains `questions.jsonl` (one JSON record per question) plus the `images/` and `videos/` assets referenced by its questions. Record fields: `id`, `source`, `question_type`, `domain`, `difficulty`, `question`, `options`, `answer`, `explanation`, `has_image`, `images`, `has_video`, `videos`, `metadata`, `major_category`, `minor_category`.

## Interactive browsing (offline-capable viewer)

`index.html` / `benchmark_viewer.html` provide the interactive question browser: category tree, search, difficulty/type/source filters, rendered questions with images and playable videos.

After cloning or downloading the repo, start a local server in the repo root:

```bash
python -m http.server 8800
```

Then open <http://localhost:8800/> in a browser. (Double-clicking the HTML file directly does not work, because browsers block `fetch()` of local files.)

GitHub Pages also works out of the box: enable Pages on this repository and the viewer is reachable at `https://<user>.github.io/PowerMMbench/`.

## Quick start

```python
import json, pathlib

# iterate over one sub-category
sub = pathlib.Path('power_grid/dispatch_operation')
for line in open(sub / 'questions.jsonl', encoding='utf-8'):
    q = json.loads(line)
    print(q['id'], q['question_type'], q['answer'])
    for img in q['images']:
        assert (sub / 'images' / img).exists()
```

## Statistics

| Major category | Sub-category | Questions | Type breakdown | Difficulty |
|---|---|---|---|---|
| **power_equipment** | power_electronics | 40 | multiple_choice 40 | medium 39, hard 1 |
|  | visual_inspection | 24 | subjective 24 | easy 12, hard 12 |
|  | rotating_machine | 20 | multiple_choice 20 | medium 20 |
|  | insulation | 16 | multiple_choice 16 | medium 15, hard 1 |
|  | partial_discharge | 15 | multiple_choice 15 | hard 15 |
|  | thermal_imaging | 12 | multiple_choice 12 | hard 12 |
|  | transformer | 9 | multiple_choice 9 | medium 9 |
|  | switchgear | 9 | multiple_choice 8, subjective 1 | medium 9 |
|  | meter_reading | 7 | multiple_choice 7 | medium 7 |
|  | cable | 5 | multiple_choice 5 | medium 5 |
| **power_grid** | dispatch_operation | 47 | multiple_choice 22, text_qa 21, time_series_analysis 3, subjective 1 | medium 44, hard 2, easy 1 |
|  | transmission_line | 30 | multiple_choice 26, time_series_analysis 3, text_qa 1 | medium 29, hard 1 |
|  | grid_topology | 19 | multiple_choice 19 | medium 19 |
|  | relay_protection | 17 | multiple_choice 10, text_qa 7 | medium 17 |
|  | power_flow | 17 | multiple_choice 10, time_series_analysis 6, text_qa 1 | medium 13, very_hard 3, easy 1 |
|  | stability_analysis | 12 | multiple_choice 8, time_series_analysis 3, text_qa 1 | medium 8, hard 3, easy 1 |
|  | fault_diagnosis | 8 | multiple_choice 8 | medium 8 |
| **demand_side** | ev_charging | 25 | multiple_choice 25 | hard 25 |
|  | load_forecasting | 18 | multiple_choice 18 | hard 16, medium 2 |
|  | user_behavior | 12 | multiple_choice 12 | hard 11, medium 1 |
|  | distributed_energy | 4 | multiple_choice 3, text_qa 1 | medium 2, hard 2 |
|  | virtual_power_plant | 2 | multiple_choice 2 | hard 2 |
|  | demand_response | 1 | multiple_choice 1 | hard 1 |
| **market_policy** | policy_regulation | 10 | multiple_choice 8, text_qa 2 | medium 10 |
|  | ancillary_service | 9 | multiple_choice 9 | hard 9 |
|  | pricing_tariff | 5 | multiple_choice 2, text_qa 2, subjective 1 | medium 5 |
|  | midlong_term | 1 | multiple_choice 1 | hard 1 |
|  | spot_market | 1 | text_qa 1 | medium 1 |
|  | carbon_green | 1 | multiple_choice 1 | hard 1 |

**Totals**: 396 questions — types: multiple_choice 317, text_qa 37, subjective 27, time_series_analysis 15; difficulty: medium 263, hard 115, easy 15, very_hard 3; 309 images; 12 videos (24 video questions).

## Sources

Questions are derived from registered electrical engineer exam archives, industry standards, PowerMMBench collection pipelines and the [ElecBench](raw_data/Elecbench) / [MMEBench](raw_data/MMEBench) data families. Per-question provenance is kept in the `metadata` and `source` fields.
