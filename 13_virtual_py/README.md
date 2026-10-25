# 📦 Module 13: Virtual Environments & Package Management

This module demonstrates how to create, activate, manage, and isolate Python dependencies using Python's built-in `venv` module and `pip`.

---

## 🎯 Why Virtual Environments?

In Python, installing packages globally (`pip install <package>`) places them into the global system directory. This causes several issues:

- **Dependency Conflicts**: Project A needs `Django 4.2`, while Project B needs `Django 5.1`. Installing globally will break one of the projects.
- **System Pollution**: Cluttering your global Python installation with dozens of experimental packages.
- **Reproducibility**: Without an isolated environment, it is difficult to determine which exact packages your project actually depends on.

Virtual environments solve this by giving each project its own isolated Python runtime, standard library copy, and `site-packages` directory.

---

## 🛠️ Step-by-Step Workflow

### 1. Creating a Virtual Environment

Use the built-in `venv` module to initialize a virtual environment:

```bash
# Create a virtual environment named .venv (standard convention)
python -m venv .venv
```

This creates a self-contained directory containing:

- `Scripts/` (Windows) or `bin/` (macOS/Linux): Python interpreter and activation scripts.
- `Lib/site-packages`: Where packages installed inside this environment will reside.
- `pyvenv.cfg`: Configuration pointing back to the base Python installation.

---

### 2. Activating the Environment

Before installing or running code with project-specific dependencies, activate the environment:

#### Windows (PowerShell):

```powershell
.\.venv\Scripts\Activate.ps1
```

> [!TIP]
> If PowerShell throws an execution policy error (`PSSecurityException`), run:
>
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```

#### Windows (Command Prompt `cmd.exe`):

```cmd
.\.venv\Scripts\activate.bat
```

#### macOS / Linux (Bash / Zsh):

```bash
source .venv/bin/activate
```

When activated, your terminal prompt will display the environment name prefix, e.g., `(.venv) PS D:\...>`

---

### 3. Inspecting & Installing Packages

```bash
# Install a package into the virtual environment
pip install pymongo django requests

# View all installed packages in table format
pip list

# View exact package versions in freeze format
pip freeze
```

---

### 4. Freezing & Replicating Dependencies

To share dependencies with team members or deploy to production:

```bash
# Export all installed package versions to a requirements file
pip freeze > requirements.txt

# In a new environment, install all listed packages exactly
pip install -r requirements.txt
```

---

### 5. Deactivating the Environment

When finished working on the project, exit the virtual environment:

```bash
deactivate
```

---

## 📁 Files in This Directory

| File               | Description                                                                                              |
| :----------------- | :------------------------------------------------------------------------------------------------------- |
| `requirements.txt` | Output of `pip list` showing packages installed in the local environment (`dnspython`, `pymongo`, etc.). |
| `requirement.txt`  | Extended environment snapshot showing additional frameworks like `Django` and `sqlparse`.                |
| `.venv/`           | Isolated Python virtual environment folder (ignored by git via `.gitignore`).                            |
