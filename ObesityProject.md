
# Project Notes: Obesity Risk Predictor
**Session Topic:** Initial Project and Git Setup  
**Purpose:** This document contains learning notes from setting up the `obesity-risk-predictor` project.

## 1. Project Overview
The goal of this project is to build an obesity risk prediction portfolio project using the **CDC BRFSS (Behavioral Risk Factor Surveillance System) Nutrition, Physical Activity & Obesity** dataset.

### Planned Project Components
* Data acquisition
* Initial inspection and exploratory data analysis (EDA)
* Data cleaning
* Feature engineering
* Gradient Boosting classification model
* Tableau dashboard
* Git/GitHub portfolio workflow

---

## 2. Project Folder Structure

### Directory Tree

```
obesity-risk-predictor/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│
├── src/
│
├── reports/
│   └── figures/
│
├── tableau/
│
├── README.md
├── requirements.txt
├── .gitignore
└── PROJECT_NOTES.md

```

### Folder & File Purposes

| Path | Purpose |
| --- | --- |
| `data/raw/` | Stores the original downloaded dataset. **Raw data should never be manually edited.** |
| `data/processed/` | Stores cleaned or transformed datasets created during the project. |
| `notebooks/` | Stores Jupyter notebooks for exploration, cleaning, modeling, and analysis. |
| `src/` | Stores reusable Python scripts/functions to be used later in the project. |
| `reports/figures/` | Stores exported plots or figures for reports, the README, or presentations. |
| `tableau/` | Stores Tableau workbooks or dashboard-related files. |
| `README.md` | Main public-facing explanation of the project. |
| `requirements.txt` | Lists Python dependencies required to run the project. |
| `.gitignore` | Tells Git which files/folders should *not* be tracked. |
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
| Enable Version Control Integration | `git init` (maps the project to Git) |
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

**The Git Workflow:** Working Files → Staging Area → Commit History

*Command Flow:* Edit files → `git status` → `git add` → `git commit`

> **IMPORTANT:** > `commit` = saves a snapshot locally
> `push` = uploads commits to GitHub

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

1. **Staged and Unstaged:** The notebook was staged once, but then modified *after* being staged. A file can exist in both the staging area and the modified area simultaneously.
2. **Untracked Files:** `.gitignore`, `README.MD`, and `requirements.txt` exist in the directory but haven't been added to Git yet.
3. **To Be Ignored:** System/IDE folders like `.idea/` and `.virtual_documents/` should be added to the `.gitignore` file so they are not committed to the repository.

---

## 5. The `.gitignore` File

The `.gitignore` file tells Git which files and folders *not* to track.

*Note: `.gitignore` controls Git tracking behavior, not program behavior.*

### Why Ignore Data Folders?

Large datasets should generally not be committed to GitHub because:

1. GitHub has strict file size limits.
2. Large files make cloning and pulling the repository slow.
3. Because Git stores the entire file history, large files remain in the repository's hidden history even if you delete them later.
4. Data should usually be downloaded directly from the official source or regenerated through documented script steps.

---

## 6. Key Takeaways & Folder Tracking

* Git tracks changes through intentional commits, not automatically forever.
* `git status` is the best command to frequently check what Git sees.
* `git init` starts a local repository.
* `.gitignore` tells Git what *not* to track.

### Git Folder Tracking and `.gitkeep`

**Git tracks files, not folders.** It does not track empty directories.

This means an empty folder like `src/` or `data/processed/` will not be pushed to GitHub. To force Git to track an empty folder so that your project structure remains intact for other users, you should create an empty hidden file inside it, conventionally named `.gitkeep`.


---

For the consolidated **Git/GitHub section**, I’d add only a few small “future-you” notes before moving on. The section is already solid, so I would not bloat it too much.

Here are the additions I’d recommend.


---

## Common Git Recovery Commands

These commands are useful when something is staged or changed by mistake.

### Unstage a File

If a file was staged with `git add` but should not be included in the next commit:

```
git restore --staged <file>
```

Example:

```
git restore --staged README.md
```

This removes the file from the staging area but keeps the file changes in the working directory.

### Discard Local Changes to a File

If a file has unwanted local edits and should be restored to the last committed version:

```
git restore <file>
```

Example:

```
git restore README.md
```

Warning:

```
This discards uncommitted changes in that file.
Use carefully.
```

### View Recent Commit History

To see recent commits in compact form:

```
git log --oneline
```

Example output:

```
8a18b3d Added Python Project Dependencies
f0abac6 Add README project sections
cb6dbf0 Add project folder placeholders
564e6b0 Initial project setup
```

---

## Practical Commit Hygiene

A commit should usually represent one logical unit of work.

Good examples:

```
Add README project sections
Add Python project dependencies
Create initial data inspection notebook
Clean CDC column names
Add obesity prevalence EDA charts
```

Avoid vague commit messages:

```
updates
stuff
changes
fix
misc
```

Avoid mixing unrelated changes in one commit, such as:

```
data cleaning + README rewrite + dashboard export + private notes cleanup
```

Better:

```
Commit 1: Clean CDC column names
Commit 2: Update README methodology section
Commit 3: Export Tableau dashboard screenshots
```

---

## Git Workflow Confidence Rule

If uncertain, run:

```
git status
```

Then read the section labels carefully:

```
Changes not staged for commit
Changes to be committed
Untracked files
Your branch is ahead of 'origin/main'
Your branch is up to date with 'origin/main'
```

These labels usually tell the next safe action.
```
