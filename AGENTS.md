# AGENTS.md

## Cursor Cloud specific instructions

This repository contains two independent research artifacts:

1. **`heterophilic_classify.ipynb`** — A Jupyter notebook for heterophilic graph node classification using PyTorch Geometric and Gurobi optimization. This is the primary runnable artifact in the Cloud Agent environment.
2. **MATLAB image resize code** — Packed in `.rar` archives; requires MATLAB (not available in Cloud Agent VMs).

### Running the notebook

- **Jupyter**: `jupyter notebook --no-browser --ip=0.0.0.0 --port=8888` from the repo root.
- The notebook was authored for Google Colab (Python 3.11). It runs on Python 3.12 with minor `DeprecationWarning`s from NumPy 2.x pickle deserialization; these are harmless.
- All Python deps are installed via the update script (`pip install --break-system-packages ...`). There is no `requirements.txt` in the repo — dependencies are inlined in notebook cells via `!pip install`.

### Gurobi license

The notebook's full optimization cells require a valid Gurobi WLS license. The credentials hardcoded in the notebook belong to the original author's academic license and will not work in other environments. Without a license, small LP models (≤2000 variables/constraints) still work. Set `GRB_WLSACCESSID`, `GRB_WLSSECRET`, and `GRB_LICENSEID` environment variables (or provide a `gurobi.lic` file) to use the full solver.

### Datasets

The notebook downloads datasets at runtime from GitHub (Planetoid, WebKB) and PyTorch Geometric's data servers (Twitch). First run requires internet access; datasets are cached under `/tmp/`.

### Linting / Testing

There is no linting configuration, test suite, or CI pipeline in this repository. The notebook is the sole runnable artifact. Validate by executing cells or running `jupyter nbconvert --to notebook --execute heterophilic_classify.ipynb` (requires a Gurobi license for full execution).

### PATH note

User-installed Python packages land in `~/.local/bin`. Ensure `PATH` includes `$HOME/.local/bin` (the update script handles this).
