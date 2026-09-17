## 1. Reproduction order (commands already in scripts/)

1. Data prep (new): `nifti_to_jpeg.py --nifti_root .../t2 --jpeg_root .../JPEG --json_log .../JPEG/nifti_to_jpeg_log.json --self_check`
2. Stage 1A reordering: `preprocessing/reordering/train.py` (see `scripts/train.sh`)
3. Stage 1B missing slices: `preprocessing/missing_slices/train.py`
4. Stage 1C combined: `preprocessing/combined/train.py` with `--pretrained_a` and `--pretrained_b`
5. Stage 2 reconstruction per resolution: `reconstruction/train.py` then `inference.py` (32, 64, 96)
6. End-to-end (Tables 1, 2): `end_to_end_pipeline.py` with the Stage 1C and Stage 2 checkpoints
7. Stage 1 component metrics (Table 3): `preprocessing/reordering/inference.py` and `preprocessing/missing_slices/inference.py`
8. Stage 3 refinement: `refinement/train.py` on the Stage 2 predictions, then `refinement/inference.py` for before/after numbers
