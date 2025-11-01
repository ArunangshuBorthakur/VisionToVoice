# VisionToVoice

VisionToVoice is a small research/code repository for experiments that map visual sign-language inputs to spoken-word targets.

Contents
--------
- `DataSet/` — annotations and metadata for the MS‑ASL dataset (see `DataSet/README.md` for detailed information and loading examples).

Quick start
-----------
1. Read the dataset notes: `DataSet/README.md` contains file descriptions and examples (JSON -> pandas DataFrame, CSV conversion, box parsing).
2. Add model and training code under a `src/` or `models/` directory and create scripts under `scripts/` for preprocessing and training.

Notes
-----
- The MS‑ASL annotations included in `DataSet/` are distributed under the Computational Use of Data Agreement (C‑UDA). See `DataSet/README.md` for citation and license reminders.
- If you'd like, I can add a minimal `scripts/convert_annotations.py` to export the JSON annotations to CSV and expand the `box` column into numeric columns.

Added/updated: 2025-11-02
