# Section 2: Python Environment and `requirements.txt`

**Purpose:** This section consolidates the Python environment setup completed for the `obesity-risk-predictor` project. The goal was to create a project-specific Python environment, install core packages for data analysis and modeling, verify the environment, securely manage secrets, and save the package list.

---

## 1. Python Version Check
Checked the installed Python version: 

```
python --version
* **Output:** `Python 3.11.14`
* **Meaning:** Python is installed, available from the terminal, and acceptable for the project.
```
To check the Python command location on this machine:
```
Get-Command python
```

*(Note: `where python` returned blank, so `Get-Command python` is more reliable in this PowerShell environment).* Before activating the virtual environment, this pointed to the global user-level install (`C:\\Users\\patri\\AppData\\Local\\Programs\\...`).

---

## 2. Creating the Virtual Environment

First, verified no existing environment (`.venv/`) was present using `dir -Force`. Then, created the virtual environment:

```
python -m venv .venv
```

* **`python`:** Use Python.
* **`-m venv`:** Run Python's built-in virtual environment module.
* **`.venv`:** Create the environment in a folder named `.venv`.

 **Mental Model:**
* **Global Python** = General/user Python installation.
* **`.venv`** = Isolated Python environment strictly for this project.

 **Important Rule:**
 The `.venv/` folder should **never** be committed to GitHub because it is local, large, and machine-specific. Instead, commit dependency files (`requirements.txt`) to document the needed packages.

---

## 3. Activating the Virtual Environment

Activated the environment in PowerShell:

```
.\\.venv\\Scripts\\Activate.ps1
```

The terminal prompt changed to include `(.venv)`, indicating the project virtual environment is active.
*(Note: This must be run every time a new terminal is opened for this project).*

Confirmed the active Python path:

```powershell
Get-Command python

```

* **Output:** `C:\\Users\\patri\\Documents\\obesity-risk-predictor\\.venv\\Scripts\\python.exe`
This ensures that packages installed now will go into the project folder, not the global installation.

---

## 4. Upgrading `pip`

Before installing packages, upgraded `pip` (Python’s package installer) inside the active environment:

```powershell
python -m pip install --upgrade pip

```

> **Best Practice:** Always use `python -m pip` instead of just `pip`. This ensures the installer is tied to the currently active Python interpreter.

---

## 5. Installing Core Dependencies

Installed core data analysis, visualization, modeling, and notebook packages:

```powershell
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter python-dotenv

```

**Main Packages & Purposes:**

| Package | Purpose |
| --- | --- |
| `pandas` | Data loading, cleaning, and tabular analysis |
| `numpy` | Numerical computing |
| `matplotlib` | Basic plotting |
| `seaborn` | Statistical visualization |
| `scikit-learn` | Machine learning models and evaluation |
| `jupyter` | Notebook support |
| `python-dotenv` | Loads environment variables/secrets from a `.env` file |

*Note: Installing these top-level packages automatically brings in many supporting dependencies (e.g., `scipy`, `joblib`, `requests`), which is completely normal.*

---

## 6. Managing Dependencies (Top-Level vs. Frozen)

### Freezing the Environment (`requirements.txt`)

Recorded the exact environment state into a file:

```powershell
python -m pip freeze > requirements.txt

```

* **`freeze`**: Lists installed packages and their exact versions from the active environment.
* **`requirements.txt`**: The standard file that stores the package list, making the environment 100% reproducible.

To recreate this exact environment in the future, one would run:

```powershell
python -m pip install -r requirements.txt

```

### Top-Level vs. Frozen Dependencies

While `requirements.txt` captures *everything* (including sub-dependencies), it can become difficult to read or update.

* **Best Practice:** Keep a separate list (often called `requirements.in` or just documented in your `README.md`) that only contains the core packages you explicitly installed (`pandas`, `scikit-learn`, etc.). This makes it much easier to upgrade your core packages in the future without causing dependency conflicts.

---

## 7. Managing Secrets (`.env` file)

When working with data, you may eventually need to use API keys to download datasets or passwords to connect to databases. These should **never** be hardcoded into your notebooks or scripts.

1. **Create a `.env` file** in the root of your project directory.
2. **Store secrets** inside it (e.g., `API_KEY=your_secret_key_here`).
3. **Load secrets** in your Python code using the `python-dotenv` package.
4. **CRITICAL:** The `.env` file must be added to your `.gitignore` file immediately so it is never pushed to GitHub.

---

## 8. Git Workflow

Checked the status to ensure `.venv/` and `.env` were ignored (thanks to `.gitignore`) and staged the new file:

```powershell
git status
git add requirements.txt
git commit -m "Added Python Project Dependencies"
git push

```

* **Result:** Local `main` and GitHub `origin/main` are synced. The working tree is clean.

---

## 9. Summary & Repeatable Workflow

**Current State:** The project now has an isolated `.venv` Python environment, verified package imports, secure secret management protocols, and a committed `requirements.txt` file that documents the environment for reproducibility.

### Repeatable Setup Workflow for Future Projects:

```powershell
python --version
python -m venv .venv
.\\.venv\\Scripts\\Activate.ps1
Get-Command python
python -m pip install --upgrade pip
python -m pip install pandas numpy matplotlib seaborn scikit-learn jupyter python-dotenv
python -m pip freeze > requirements.txt
git status
git add requirements.txt
git commit -m "Add Python project dependencies"
git push
git status

```

### Golden Rules:

1. **Activate `.venv**` before starting project work (`.\\.venv\\Scripts\\Activate.ps1`).
2. **Confirm active Python** if unsure (`Get-Command python`).
3. **Use `python -m pip**` instead of just `pip`.
4. **Update `requirements.txt**` after any dependency changes (`python -m pip freeze > requirements.txt`).
5. **Commit `requirements.txt**`.
6. **NEVER commit `.venv/` or `.env**`.

```
