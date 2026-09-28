# PowerMMBench

**PowerMMBench** is a multimodal benchmark for evaluating large language models (LLMs / VLMs) in the power & energy domain, with **396 questions** across 4 major categories (power equipment, power grid, demand side, market & policy), 29 sub-categories, and four modalities (text, image, time series, video).

## Repository layout

| Folder | Content |
|---|---|
| [`PowerMMBench/`](PowerMMBench) | The benchmark itself: 396 questions with images and videos, nested by major category / sub-category |
| [`Elecbench/`](Elecbench) | Raw data of **ElecBench** (IEEE PESGM 2025 Best Paper), a power-dispatch evaluation benchmark: 4 test sets (general / monitoring / dispatch / blackstart), 288 questions |
| [`MMEBench/`](MMEBench) | MMEBench annotations and power-electronics industry images |

## Quick start

```python
import json, pathlib

# iterate over one sub-category
sub = pathlib.Path('PowerMMBench/power_grid/dispatch_operation')
for line in open(sub / 'questions.jsonl', encoding='utf-8'):
    q = json.loads(line)
    print(q['id'], q['question_type'], q['answer'])
    for img in q['images']:
        assert (sub / 'images' / img).exists()
```

See [PowerMMBench/README.md](PowerMMBench/README.md) for the full category tree and statistics.
