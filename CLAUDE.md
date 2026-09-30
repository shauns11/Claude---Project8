###############################
#CLAUDE.md (Project8)
###############################
  
# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

Execute a Jupyter Notebook file (extension .ipynb) using Visual Studio Code. 
No dataset is needed for this task. There is no .ipynb file. 
The task involves opening a new Jupyter Notebook file, running a basic script, and saving the new notebook in the `code\` folder.

## File Paths

- Working directory: `C:\CLAUDE\Projects\Project8`
- Notebook files: `code\`
- Log files, tables, figures: `output\`
- Datasets: `data\`
- Examples of notebook files: `examples\`

## Running a notebook script in VSC

- Within VSC create a new Jupyter Notebook file (extension .ipynb) 
- Place the commands below in the notebook file

```python
import pandas as pd
import numpy as np
print(2 + 2)
from datetime import datetime
now = datetime.now()
print("Date and time:", now.strftime("%Y-%m-%d %H:%M:%S"))
```

- Run the new notebook file from within VSC.
- Save the notebook file in the code folder within the working directory with a descriptive filename (e.g. add_two_numbers.ipynb)


Verify the expected `.ipynb` file exists in `code\` before reporting the task as complete.

## Enable CLAUDE to create / edit notebook files in VSC

- If necessary, please create settings.json within the Project8 folder so that claude can create/edit files and perform common filesystem operations such as creating directories without repeatedly asking you. Please add steps necessary to perform task in the CLAUDE.file

- `.claude\settings.json` (project-level) has been created with permissions allowing Claude to Read/Write/Edit any file under `C:\CLAUDE\Projects\Project8\`, create directories under the project, and run `python`, `jupyter`, and `pip install` commands without prompting each time. 

### How notebook execution was actually performed

Claude Code runs headless (no GUI), so it cannot literally click "Run" inside the VS Code Jupyter extension. Instead, the notebook is executed with the equivalent CLI tool that VS Code's Jupyter extension itself calls under the hood (same kernel, same outputs):

```
python -m nbconvert --to notebook --execute --inplace "code\<name>.ipynb"
```

This runs every cell against a real Python kernel and writes the outputs back into the `.ipynb` file in place, so opening the file afterward in VS Code shows already-executed cells. Required packages confirmed present on this machine: `pandas`, `numpy`, `ipykernel`, `nbconvert`, `nbclient`, `nbformat`.

Steps to reproduce the task:
1. Write a new `.ipynb` file into `code\` containing the desired code cell(s) (nbformat 4 JSON).
2. Run the `nbconvert --execute --inplace` command above to execute it and populate outputs.
3. Verify the file exists in `code\` and that outputs were populated (no error traceback in the cell output).

## Directory Layout

- `code\` — Python scripts and notebooks (e.g. `add_two_numbers.ipynb`)
- `output\` — generated files: logs, tables, figures
- `data\` — input datasets


## Script Template

```python
# Libraries
import pandas as pd

# Commands
# ... analysis code ...

# Timestamp
import datetime
print(f"Program completed on: {datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
```

## Additions to CLAUDE.md

Please add any settings necessary to complete this task to the CLAUDE.md file so that claude can create/edit files and perform common filesystem operations such as creating directories without repeatedly asking you. Please add steps necessary to perform task in the CLAUDE.file

## Examples

Example code is provided in "C:\CLAUDE\Projects\Project8\examples\operators_in_pythonNotebook.ipynb"

## Git and GitHub

Remote: `https://github.com/shauns11/Claude---Project8.git` (branch `main`). The GitHub CLI (`gh`) is not installed, so use plain `git` and the GitHub website.

### First-time setup (new project)

1. Create `.gitignore` in the project root **before** the first commit, so ignored files are never committed:

```text
# Secondary logs created by batch mode (/e) in the project root
/*.log

# Stata datasets (anywhere in the project)
*.dta

# R datasets (anywhere in the project)
*.rds

# Claude Code local settings
.claude/settings.json
```

2. Initialise the repository, check what will and won't be committed, then commit:

```powershell
git init -b main
git add .
git status --short             # files to be committed
git status --short --ignored   # lines starting "!!" are ignored (e.g. 01.log)
git commit -m "Initial commit"
```

3. Create an **empty** repository on github.com (no README, .gitignore or licence) and choose Public or Private.
4. Before pushing, confirm the remote exists and is empty. `git ls-remote` returns nothing for an empty repo and "Repository not found" if the URL is wrong, deleted or private without access:

```powershell
git ls-remote https://github.com/shauns11/Claude---Project8.git
```

5. Add the remote and push `main`:

```powershell
git remote add origin https://github.com/shauns11/Claude---Project8.git
git push -u origin main
git status -sb                 # should show: ## main...origin/main
```

6. Update the `Remote:` line at the top of this section.

Notes:
- Never use `git push --force` against a repository that already has history unless you intend to permanently replace it.
- Warnings like "LF will be replaced by CRLF" are Windows line-ending notices and can be ignored.

### Day-to-day

```powershell
git status                 # see what changed
git add .                  # stage changes
git commit -m "Message"    # commit
git push                   # upload to GitHub
```

### What is tracked

- Tracked: `code\` (Python notebooks .ipynb), `output\` (logs, tables, figures), `CLAUDE.md`, `.gitignore`
- Ignored (see `.gitignore`):
  - `/*.log` — root-level logs created by batch mode
  - `*.dta` — Stata datasets, anywhere in the project
  - `*.rds` — R datasets, anywhere in the project
  - `.claude/settings.json` — Claude Code local permission settings (kept on disk, not uploaded)

