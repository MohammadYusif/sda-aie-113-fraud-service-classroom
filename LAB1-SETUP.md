# Lab 1 — Environment Setup

Do this before starting the tasks in `LAB1.md`.

## 1. You're already at the starting point

This repo starts exactly where Lab 1 begins — just clone it, no checkout
needed:

```bash
git clone <this-repo-url>
cd <repo-folder>
```

## 2. Create a virtual environment (first time only)

This is the **one venv you'll reuse for the entire course** — every later
lab activates this same one, it's never recreated.

**Windows (PowerShell)**
```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```
If PowerShell refuses to run the activation script (`running scripts is
disabled on this system`), run this once first, then retry activation:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

**macOS / Linux**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

Your prompt should now start with `(.venv)`. Every command below assumes
it's activated — if you close and reopen your terminal, re-run only the
activation line (not `python -m venv .venv` again).

## 3. Install dependencies

At this checkpoint `pyproject.toml` doesn't have a `[build-system]` section
yet — that's part of your Lab 1 task, so `pip install -e .` won't work
until you've written it. For now, install from the repo's pinned lock file
instead of naming packages directly:

```bash
pip install -r requirements.lock
pip install ipykernel
```

**Always install from `requirements.lock`, not `pip install scikit-learn`
by itself.** `models/fraud_xgb_v3.joblib` was pickled with an exact
scikit-learn version, and `requirements.lock` pins that same version
(currently 1.9.0). A newer or older scikit-learn can silently score things
differently, or crash outright when you write the golden-score/AUC tests in
Lab 4 — scikit-learn's own `InconsistentVersionWarning` exists precisely
because this happens. This lock file already has everything every later
lab needs too, so you won't hit this again as the course adds dependencies.

(`ipykernel` is only there so VS Code's notebook UI can find this venv as a
kernel — it's not a project dependency, so it isn't in the lock file.)

## 4. Verify

Open `notebook_v1.ipynb` in VS Code, click the kernel picker top-right, and
select the `.venv` you just created (it'll usually show as `.venv
(Python 3.12.x)`). Run all cells top to bottom — it should finish without
errors and print scored counts.

## Troubleshooting

- **Wrong Python picked up / `pandas` not found**: check VS Code's kernel
  picker is actually pointing at `.venv`, not a system Python or a
  different environment.
- **`python` not found**: try `python3`, or `py` on Windows.
