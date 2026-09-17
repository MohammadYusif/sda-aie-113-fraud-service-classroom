# Lab 6 — Environment Setup

Do this before starting the tasks in `LAB6.md`.

## 1. Continue from Lab 5

Stay on `main`, continuing from your Lab 5 commit. No checkout needed.

## 2. Activate your venv

Same `.venv` as before.

**Windows (PowerShell)**
```powershell
.venv\Scripts\Activate.ps1
```

**macOS / Linux**
```bash
source .venv/bin/activate
```

## 3. Install dependencies

This lab needs `pydantic-settings` and `structlog`, which haven't come up
yet:

```bash
pip install pydantic-settings structlog
```

If you're picking this repo up fresh (new machine, new clone), run
`pip install -r requirements.lock` first — as in every lab from here
back, this keeps `scikit-learn` pinned to the exact version
`models/fraud_xgb_v3.joblib` was pickled with, not whatever an unpinned
install would otherwise resolve.

## 4. Verify

```bash
python -c "import pydantic_settings, structlog; print('ok')"
```
should print `ok` with no import errors.

## 5. Secret-scanning tool

This lab includes a real secret-leak drill using `gitleaks`. Install it
before you reach that task:

- Windows: `choco install gitleaks` (or download the binary from its
  GitHub releases page)
- macOS: `brew install gitleaks`
- Linux: download the binary from the `gitleaks` GitHub releases page

Confirm it's on your PATH:
```bash
gitleaks version
```
