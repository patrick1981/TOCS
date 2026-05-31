# Project Notes: Obesity Risk Predictor

**Session Topic:** Initial Project and Git Setup  
**Purpose:** This document contains learning notes from setting up the obesity-risk-predictor project.

---

## 1. Project Overview
The goal of this project is to build an obesity risk prediction portfolio project using the CDC BRFSS (Behavioral Risk Factor Surveillance System) Nutrition, Physical Activity & Obesity dataset.

### Planned Project Components
* Data acquisition
* Initial inspection and exploratory data analysis (EDA)
* Data cleaning
* Feature engineering
* Gradient Boosting classification model
* Tableau dashboard
* Git/GitHub portfolio workflow

### Data Source Details
* **Dataset:** CDC BRFSS Nutrition, Physical Activity & Obesity
* **Download URL:** `[INSERT SPECIFIC CDC URL HERE — e.g., https://www.cdc.gov/brfss/annual_data/annual_2022.htm]`
* **Download Date:** 2026-05-31
* **Version/Year:** `[VERIFY YEAR UPON DOWNLOAD — e.g., 2022]`
* **Reproducibility Note:** If the CDC link changes or is archived, the raw data must be re-downloaded from the official CDC archive. Do not rely on cached copies alone for long-term reproducibility. Record the URL and version in the README as well.

### Model Evaluation Strategy
* **Primary Metric:** **F1-Score** or **ROC-AUC** (preferred over Accuracy due to likely class imbalance in obesity prevalence across the population).
* **Secondary Metrics:** Precision and Recall (to understand the trade-off between false positives and false negatives in a health risk predictor — misclassifying an at-risk individual as not-at-risk carries different consequences than the reverse).
* **Validation Strategy:** Stratified K-Fold Cross-Validation to ensure class distribution is maintained across each fold. This matters because the obesity classes may not be evenly represented in the BRFSS sample.
* **Rationale:** For medical/risk prediction tasks, Accuracy is often misleading. If 70% of the population is non-obese, a naive model predicting "not obese" for everyone achieves 70% accuracy while being clinically useless. F1 and ROC-AUC penalize this kind of degenerate solution.

### Tableau Dashboard Data Connection Strategy
* **Connection Method:** `[DECIDE AND RECORD — e.g., Import processed CSV directly into Tableau Desktop, or publish processed data to Tableau Server/Public.]`
* **Data Preparation Implications:** If connecting via CSV, the `data/processed/` folder must contain a final, clean, analysis-ready dataset that Tableau will consume. Aggregation and calculated fields should be handled in Tableau where possible, but pre-aggregated summary tables may also be exported from notebooks for dashboard performance.
* **Why This Matters Now:** The way Tableau connects to data affects downstream decisions in the cleaning and feature engineering pipeline. Recording this early avoids rework.

---

## 2. Project Folder Structure

### Directory Tree
```text
obesity-risk-predictor/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
├── src/
├── reports/
│   └── figures/
├── tableau/
│
├── README.md
├── requirements.txt
├── .gitignore
├── LICENSE
└── PROJECT_NOTES.md

```

### Folder & File Purposes

| Path | Purpose |
| --- | --- |
| `data/raw/` | Stores the original downloaded dataset. Raw data should never be manually edited. |
| `data/processed/` | Stores cleaned or transformed datasets created during the project. |
| `notebooks/` | Stores Jupyter notebooks for exploration, cleaning, modeling, and analysis. |
| `src/` | Stores reusable Python scripts/functions to be used later in the project. |
| `reports/figures/` | Stores exported plots or figures for reports, the README, or presentations. |
| `tableau/` | Stores Tableau workbooks or dashboard-related files. |
| `README.md` | Main public-facing explanation of the project. |
| `requirements.txt` | Lists Python dependencies required to run the project. |
| `.gitignore` | Tells Git which files/folders should not be tracked. |
| `LICENSE` | Defines the license under which the project is shared (MIT recommended for portfolios). |
| `PROJECT_NOTES.md` | Personal learning notes for the project (this document). |

---

## 3. Git Concepts Learned

### Git vs. GitHub

| Tool | Definition |
| --- | --- |
| **Git** | Version control software installed locally on your computer. Tracks changes locally. |
| **GitHub** | Website/cloud platform for hosting Git repositories online. |

### PyCharm Actions vs. Git Commands

| PyCharm Action | Git Command Equivalent |
| --- | --- |
| Enable Version Control Integration | `git init` |
| Add/Stage file | `git add <file>` |
| Commit | `git commit` |
| Push | `git push` |
| Pull | `git pull` |
| View history | `git log` |

### Git Status Concepts

| State | Meaning |
| --- | --- |
| **Untracked** | Git sees the file, but it is not tracking it yet. |
| **Modified** | Git is tracking the file, and it has changed since the last commit/stage. |
| **Staged** | The file is marked to be included in the next commit. |
| **Committed** | The file snapshot has been saved in the Git history. |

### The Git Workflow

Working Files → Staging Area → Commit History

* **Command Flow:** Edit files → `git status` → `git add` → `git commit`

> **IMPORTANT:** `commit` = saves a snapshot locally | `push` = uploads commits to GitHub

### Common Git Recovery Commands

These commands are useful when something is staged or changed by mistake.

**1. Unstage a File**
If a file was staged with `git add` but should not be included in the next commit:

```bash
git restore --staged <file>

```

* *Example:* `git restore --staged README.md`
* *Effect:* Removes the file from the staging area but keeps the file changes in the working directory.

**2. Discard Local Changes to a File**
If a file has unwanted local edits and should be restored to the last committed version:

```bash
git restore <file>

```

* *Example:* `git restore README.md`
* *Warning:* This discards uncommitted changes in that file. Use carefully.

**3. View Recent Commit History**
To see recent commits in compact form:

```bash
git log --oneline

```

* *Example output:*
```text
8a18b3d Added Python Project Dependencies
f0abac6 Add README project sections
cb6dbf0 Add project folder placeholders
564e6b0 Initial project setup

```



### Practical Commit Hygiene

A commit should usually represent one logical unit of work.

**Good Examples:**

* "Add README project sections"
* "Add Python project dependencies"
* "Create initial data inspection notebook"
* "Clean CDC column names"
* "Add obesity prevalence EDA charts"

**Avoid vague commit messages:**

* *updates, stuff, changes, fix, misc*

**Avoid mixing unrelated changes in one commit:**

* **BAD:** data cleaning + README rewrite + dashboard export + private notes cleanup
* **BETTER:**
* Commit 1: Clean CDC column names
* Commit 2: Update README methodology section
* Commit 3: Export Tableau dashboard screenshots



### Git Workflow Confidence Rule

If uncertain, run:

```bash
git status

```

Then read the section labels carefully:

* *Changes not staged for commit*
* *Changes to be committed*
* *Untracked files*
* *Your branch is ahead of 'origin/main'*
* *Your branch is up to date with 'origin/main'*

These labels usually tell the next safe action.

---

## 4. Current Git Status Observations

At one point, running `git status` output the following:

```text
On branch main
No commits yet

Changes to be committed:
  new file: notebooks/01_data_acquisition_and_initial_inspection.ipynb

Changes not staged for commit:
  modified: notebooks/01_data_acquisition_and_initial_inspection.ipynb

Untracked files:
  .gitignore
  .idea/
  .virtual_documents/
  README.MD
  requirements.txt

```

**Interpretation & Lessons:**

* **Staged and Unstaged:** The notebook was staged once, but then modified after being staged. A file can exist in both the staging area and the modified area simultaneously.
* **Untracked Files:** `.gitignore`, `README.MD`, and `requirements.txt` exist in the directory but haven't been added to Git yet.
* **To Be Ignored:** System/IDE folders like `.idea/` and `.virtual_documents/` should be added to the `.gitignore` file so they are not committed to the repository.

---

## 5. The .gitignore File

The `.gitignore` file tells Git which files and folders **not** to track.

> *Note: `.gitignore` controls Git tracking behavior, not program behavior.*

### Why Ignore Data Folders?

Large datasets should generally not be committed to GitHub because:

1. GitHub has strict file size limits.
2. Large files make cloning and pulling the repository slow.
3. Because Git stores the entire file history, large files remain in the repository's hidden history even if you delete them later.

Data should usually be downloaded directly from the official source or regenerated through documented script steps.

### Current .gitignore Entries (Maintained List)

* `.venv/` — Local virtual environment (machine-specific, large)
* `.env` — Secrets file (API keys, passwords — NEVER commit)
* `.idea/` — PyCharm IDE configuration
* `.virtual_documents/` — Jupyter virtual document artifacts
* `data/raw/` — Large raw datasets
* `data/processed/` — Regeneratable processed datasets
* `__pycache__/` — Python bytecode cache
* `.DS_Store` — macOS filesystem metadata
* `*.ipynb_checkpoints/` — Jupyter notebook auto-save checkpoints

---

## 6. Key Takeaways & Folder Tracking

* Git tracks changes through intentional commits, not automatically forever.
* `git status` is the best command to frequently check what Git sees.
* `git init` starts a local repository.
* `.gitignore` tells Git what not to track.

### Git Folder Tracking and `.gitkeep`

Git tracks files, not folders. It does not track empty directories.

This means an empty folder like `src/` or `data/processed/` will not be pushed to GitHub. To force Git to track an empty folder so that your project structure remains intact for other users, you should create an empty hidden file inside it, conventionally named `.gitkeep`.

---

# Part 2: Python Environment and requirements.txt

**Purpose:** This section consolidates the Python environment setup completed for the obesity-risk-predictor project. The goal was to create a project-specific Python environment, install core packages for data analysis and modeling, verify the environment, securely manage secrets, and save the package list.

## 1. Python Version Check

Checked the installed Python version:

```bash
python --version

```

* **Output:** `Python 3.11.14`
* **Meaning:** Python is installed, available from the terminal, and acceptable for the project.

To check the Python command location on this machine:

```powershell
Get-Command python

```

*(Note: `where python` returned blank, so `Get-Command python` is more reliable in this PowerShell environment). Before activating the virtual environment, this pointed to the global user-level install (`C:\Users\patri\AppData\Local\Programs...`).*

**Python Version Pinning Note:**
The Python version (3.11.14) is NOT recorded in `requirements.txt`. For full reproducibility, document the Python version in the README and consider adding a `.python-version` file (used by pyenv and some CI tools) containing simply: `3.11.14`

## 2. Creating the Virtual Environment

First, verified no existing environment (`.venv/`) was present using `dir -Force`. Then, created the virtual environment:

```bash
python -m venv .venv

```

* `python`: Use Python.
* `-m venv`: Run Python's built-in virtual environment module.
* `.venv`: Create the environment in a folder named `.venv`.

**Mental Model:**

* **Global Python:** General/user Python installation.
* **.venv:** Isolated Python environment strictly for this project.

> **Important Rule:** The `.venv/` folder should never be committed to GitHub because it is local, large, and machine-specific. Instead, commit dependency files (`requirements.txt`) to document the needed packages.

## 3. Activating the Virtual Environment

Activated the environment in PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1

```

The terminal prompt changed to include `(.venv)`, indicating the project virtual environment is active. *(Note: This must be run every time a new terminal is opened for this project).*

Confirmed the active Python path:

```powershell
Get-Command python

```

* **Output:** `C:\Users\patri\Documents\obesity-risk-predictor\.venv\Scripts\python.exe`
This ensures that packages installed now will go into the project folder, not the global installation.

### Cross-Platform Activation Commands

* **PowerShell (Windows):** `.\.venv\Scripts\Activate.ps1`
* **Command Prompt (Windows):** `.venv\Scripts\activate.bat`
* **Bash/Zsh (macOS/Linux):** `source .venv/bin/activate`

*Verification:* Run `Get-Command python` (PowerShell) or `which python` (Bash/macOS/Linux) to confirm the path points to `.venv`.

*Why This Matters:* If you switch machines, use WSL, or collaborate with someone on macOS/Linux, the activation command differs. The rest of the workflow (`pip install`, `python` commands) is identical across platforms.

## 4. Upgrading pip

Before installing packages, upgraded pip (Python's package installer) inside the active environment:

```bash
python -m pip install --upgrade pip

```

*Best Practice:* Always use `python -m pip` instead of just `pip`. This ensures the installer is tied to the currently active Python interpreter.

## 5. Installing Core Dependencies

Installed core data analysis, visualization, modeling, and notebook packages:

```bash
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter python-dotenv

```

### Main Packages & Purposes

| Package | Purpose |
| --- | --- |
| **pandas** | Data loading, cleaning, and tabular analysis |
| **numpy** | Numerical computing |
| **matplotlib** | Basic plotting |
| **seaborn** | Statistical visualization |
| **scikit-learn** | Machine learning models and evaluation |
| **jupyter** | Notebook support |
| **python-dotenv** | Loads environment variables/secrets from a `.env` file |

*(Note: Installing these top-level packages automatically brings in many supporting dependencies (e.g., scipy, joblib, requests), which is completely normal).*

## 6. Managing Dependencies (Top-Level vs. Frozen)

### Freezing the Environment (`requirements.txt`)

Recorded the exact environment state into a file:

```bash
python -m pip freeze > requirements.txt

```

* `freeze`: Lists installed packages and their exact versions from the active environment.
* `requirements.txt`: The standard file that stores the package list, making the environment 100% reproducible.

To recreate this exact environment in the future, one would run:

```bash
python -m pip install -r requirements.txt

```

### Top-Level vs. Frozen Dependencies

While `requirements.txt` captures everything (including sub-dependencies), it can become difficult to read or update.

*Best Practice:* Keep a separate list (often called `requirements.in` or just documented in your `README.md`) that only contains the core packages you explicitly installed. This makes it much easier to upgrade your core packages in the future without causing dependency conflicts.

**Alternative — pip-tools:**
For a more robust workflow, consider using pip-tools (`pip install pip-tools`), which provides:

* `pip-compile`: Generates a fully resolved `requirements.txt` from a minimal `requirements.in`.
* `pip-sync`: Installs exactly what is in `requirements.txt` (removing extras).

## 7. Managing Secrets (`.env` file)

When working with data, you may eventually need to use API keys to download datasets or passwords to connect to databases. These should never be hardcoded into your notebooks or scripts.

1. Create a `.env` file in the root of your project directory.
2. Store secrets inside it (e.g., `API_KEY=your_secret_key_here`).
3. Load secrets in your Python code using the `python-dotenv` package.

> **CRITICAL:** The `.env` file must be added to your `.gitignore` file immediately so it is never pushed to GitHub.

**Loading Secrets in Python (Example):**

```python
from dotenv import load_dotenv
import os

load_dotenv()  # Loads variables from .env into environment
api_key = os.getenv("API_KEY")

```

**Security Reminder:** If a secret is accidentally committed and pushed, simply deleting it in a later commit does NOT remove it from Git history. You would need to rewrite history (`git filter-branch` or BFG Repo-Cleaner) or rotate the compromised credential. Prevention is far cheaper than remediation.

## 8. Git Workflow

Checked the status to ensure `.venv/` and `.env` were ignored (thanks to `.gitignore`) and staged the new file:

```bash
git status
git add requirements.txt
git commit -m "Added Python Project Dependencies"
git push

```

*Result:* Local `main` and GitHub `origin/main` are synced. The working tree is clean.

## 9. Summary & Repeatable Workflow

**Current State:** The project now has an isolated `.venv` Python environment, verified package imports, secure secret management protocols, and a committed `requirements.txt` file that documents the environment for reproducibility.

### Repeatable Setup Workflow for Future Projects:

```bash
python --version
python -m venv .venv

.\.venv\Scripts\Activate.ps1                    # Windows PowerShell
# OR: source .venv/bin/activate                  # macOS/Linux

Get-Command python                               # Verify path points to .venv
python -m pip install --upgrade pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter python-dotenv
python -m pip freeze > requirements.txt

git status
git add requirements.txt
git commit -m "Add Python project dependencies"
git push
git status

```

### Golden Rules

1. Activate `.venv` before starting project work (`.\.venv\Scripts\Activate.ps1`).
2. Confirm active Python if unsure (`Get-Command python`).
3. Always ensure pip is up to date (`python -m pip install --upgrade pip`).
4. Use `python -m pip` instead of just `pip`.
5. Update `requirements.txt` after any dependency changes (`python -m pip freeze > requirements.txt`).
6. Commit `requirements.txt`.
7. **NEVER commit `.venv/` or `.env`.**
8. Document the exact data source URL, version, and download date.
9. Choose evaluation metrics before building the model — not after.
10. Add a LICENSE file before publishing a portfolio repository.

```
