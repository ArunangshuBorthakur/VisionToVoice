MS-ASL: A Large-Scale Data Set and Benchmark for Understanding American Sign Language
============================================================================================

This package containing the `MS-ASL dataset`, as proposed in MS-ASL: A Large-Scale Data Set and Benchmark for Understanding American Sign Language paper.  
For more information visit [the website](https://www.microsoft.com/en-us/research/project/ms-asl/).


# MS‑ASL (MS‑American Sign Language) — dataset bundle

This folder contains the MS‑ASL annotation files (downloaded from the official MS‑ASL release) used for sign language classification experiments.

For the original paper and dataset details, see: https://www.microsoft.com/en-us/research/project/ms-asl/

Summary of included files
-------------------------
The dataset folder should contain the following annotation files (JSON):

- `MSASL_train.json` — training samples
- `MSASL_val.json` — validation samples
- `MSASL_test.json` — test samples
- `MSASL_classes.json` — class index to gloss mapping (e.g. 0 -> "hello")
- `MSASL_synonym.json` — lists of synonyms grouped to a single class

Note: if you have additional files (e.g. a CSV export or the C‑UDA license PDF), place them in this folder and update this README if you want them referenced explicitly.

Data format / sample structure
-----------------------------
Each sample in the train/test/val files is an annotation object with fields similar to:

{
  "url": "http://...",
  "start_time": 12.34,
  "end_time": 14.56,
  "label": 123,
  "signer_id": "s123",
  "box": [y0, x0, y1, x1],
  "text": "gloss",
  "width": 1280,
  "height": 720,
  "fps": 30
}

- `label` is an integer class id (0..N-1) that maps to a gloss in `MSASL_classes.json`.
- `box` is a normalized bounding box [y0, x0, y1, x1] (values in [0,1]).

Subsets
-------
The dataset supports common subsets used in the MS‑ASL paper (MS‑ASL100, 200, 500, 1000). To obtain a subset, filter samples where `label < K` (e.g. use `label < 100` for MS‑ASL100).

How to load (quick examples)
----------------------------
Python (load JSON and create a pandas DataFrame):

```python
import json
import pandas as pd

# load file
with open('DataSet/MSASL_train.json', 'r', encoding='utf-8') as f:
    data = json.load(f)

# data is typically a list of dicts
df = pd.DataFrame(data)
print(df.shape)
print(df.columns.tolist())

# convert to CSV if desired
df.to_csv('DataSet/MSASL_train.csv', index=False)
```

If you already have a CSV, load it with `pd.read_csv('DataSet/yourfile.csv')`. Note that the `box` column may be stored as a list or as a string — you may need to parse it (e.g. `ast.literal_eval`) and expand into numeric columns `y0,x0,y1,x1`.

Example: expand `box` into numeric columns

```python
import ast
boxes = df['box'].apply(lambda s: ast.literal_eval(s) if isinstance(s, str) else s)
df[['y0','x0','y1','x1']] = pd.DataFrame(boxes.tolist(), index=df.index)
```

Citation & license
-------------------
If you use MS‑ASL in your work please cite the original paper:

@InProceedings{vaezijoze2019ms-asl,
  author    = {Vaezi Joze, Hamid Reza and Koller, Oscar},
  title     = {MS-ASL: A Large-Scale Data Set and Benchmark for Understanding American Sign Language},
  booktitle = {The British Machine Vision Conference (BMVC)},
  year      = {2019}
}

The dataset is distributed under the Computational Use of Data Agreement (C‑UDA). Follow the license terms that accompany the dataset (if a `C-UDA` PDF is included, consult it for details).

Contacts
--------
- Hamid Vaezi Joze — https://www.microsoft.com/en-us/research/people/hava/
- Oscar Koller — https://www.microsoft.com/en-us/research/people/oskoller/

Notes / next steps
------------------
- If you want, I can:
  - add the exact CSV filename into this README if you provide it, or
  - add a small helper script `scripts/convert_annotations.py` that converts JSON -> CSV and normalizes `box` columns.
  - add an example that prints per-class counts/useful stats.

Added/updated: 2025-11-02


