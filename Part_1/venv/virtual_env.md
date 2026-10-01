# Python Virtual Environments

## 1. What is a Python Environment?

A Python environment is the setup in which Python code runs.

It contains:

- Python itself
- Installed packages
- Package versions
- Dependencies required by a project

For example, one project may require:

```text
pandas
numpy
scikit-learn
```

while another project may require different packages or different versions.

If everything is installed globally, different projects can interfere with each other.

This is why we use **virtual environments**.

---

# 2. What is a Virtual Environment?

A **virtual environment** is an isolated Python environment created for a particular project.

It allows each project to have its own:

- Python packages
- Package versions
- Dependencies

without affecting other projects or the system-wide Python installation.

### Example

Suppose:

```text
Project A → pandas 2.x
Project B → pandas 1.x
```

Installing both globally can create dependency problems.

With virtual environments:

```text
Project A
└── .venv
    └── pandas 2.x

Project B
└── .venv
    └── pandas 1.x
```

Both projects can work independently.

---

# 3. Why Virtual Environments Matter

Virtual environments are useful because they provide:

### Isolation

Packages installed for one project do not normally affect another project.

### Dependency Management

Each project can use the package versions it needs.

### Reproducibility

A project can record its dependencies so another person can recreate the environment.

### Cleaner System

You avoid installing every project dependency globally.

---

# 4. Creating a Virtual Environment

First, navigate to your project directory:

```powershell
cd path/to/project
```

Then create the virtual environment:

```powershell
python -m venv .venv
```

### What does this command mean?

```text
python
```

Runs Python.

```text
-m venv
```

Runs Python's built-in `venv` module.

```text
.venv
```

Is the name of the virtual environment directory.

So:

```powershell
python -m venv .venv
```

means:

> Create a virtual environment named `.venv` in the current project directory.

---

# 5. What Does `.venv` Mean?

`.venv` is simply a commonly used name for the virtual environment directory.

You could technically use another name:

```powershell
python -m venv myenv
```

But `.venv` is commonly used because it clearly indicates:

> This directory contains the project's virtual environment.

The leading `.` also makes it a hidden-style project directory on systems that treat dot-prefixed names specially.

---

# 6. Activating the Virtual Environment

After creating the environment, we activate it.

## Windows PowerShell

```powershell
.venv\Scripts\Activate.ps1
```

After activation, your terminal usually shows:

```text
(.venv) PS C:\Users\sahul\Desktop\project>
```

The:

```text
(.venv)
```

indicates that the virtual environment is currently active.

---

# 7. Activating on Windows Command Prompt

If you are using Command Prompt instead of PowerShell:

```cmd
.venv\Scripts\activate
```

---

# 8. Activating on Linux/macOS

On Linux or macOS:

```bash
source .venv/bin/activate
```

---

# 9. Checking Whether the Environment is Active

One simple way is to look at the terminal prompt.

For example:

```text
(.venv) PS C:\Users\sahul\Desktop\Winter_ARC>
```

The:

```text
(.venv)
```

shows that the virtual environment is active.

You can also check which Python executable is being used.

### Windows

```powershell
where python
```

### Linux/macOS

```bash
which python
```

When the virtual environment is active, Python should point to the `.venv` environment.

---

# 10. Installing Packages

Once the virtual environment is activated, you can install packages using `pip`.

For example:

```powershell
pip install pandas
```

Install multiple packages:

```powershell
pip install pandas numpy scikit-learn
```

These packages are installed into the active virtual environment.

---

# 11. What is pip?

`pip` is Python's package installer.

It is used to:

- Install packages
- Upgrade packages
- Remove packages
- View installed packages
- Install dependencies from a requirements file

For example:

```powershell
pip install pandas
```

installs pandas.

---

# 12. Checking Installed Packages

Use:

```powershell
pip list
```

This displays the packages installed in the current environment.

Example:

```text
Package      Version
------------ -------
numpy        ...
pandas       ...
scikit-learn ...
```

---

# 13. Checking Information About a Package

You can use:

```powershell
pip show pandas
```

This provides information about the installed package.

For example, it can show:

- Package name
- Version
- Location
- Dependencies

---

# 14. Uninstalling a Package

To remove a package:

```powershell
pip uninstall pandas
```

`pip` will normally ask for confirmation.

---

# 15. Upgrading a Package

To upgrade a package:

```powershell
pip install --upgrade pandas
```

This tells `pip` to install a newer available version.

---

# 16. requirements.txt

A project often needs several Python packages.

Instead of manually telling someone:

```text
Install pandas
Install numpy
Install scikit-learn
...
```

we can create a file called:

```text
requirements.txt
```

This file contains the project's dependencies.

Example:

```text
pandas
numpy
scikit-learn
```

---

# 17. Creating requirements.txt

If your virtual environment already contains the packages required by your project, you can generate a requirements file using:

```powershell
pip freeze > requirements.txt
```

### What does this do?

```text
pip freeze
```

lists the installed packages and their versions.

```text
>
```

redirects the output into a file.

```text
requirements.txt
```

is the file where the dependencies are stored.

For example:

```text
numpy==2.x.x
pandas==2.x.x
scikit-learn==1.x.x
```

The exact versions depend on what is installed in your environment.

---

# 18. Installing from requirements.txt

Suppose someone gives you a project containing:

```text
requirements.txt
```

You can recreate the required dependencies using:

```powershell
pip install -r requirements.txt
```

### What does `-r` mean?

`-r` tells `pip`:

> Read the package requirements from this file.

So:

```powershell
pip install -r requirements.txt
```

means:

> Install all packages listed in `requirements.txt`.

---

# 19. Recreating an Environment

Suppose someone gives you a project:

```text
my-project/
│
├── .venv/
├── main.py
├── requirements.txt
└── README.md
```

You normally **do not need to copy their `.venv` directory**.

Instead, create your own environment:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Then install the project's dependencies:

```powershell
pip install -r requirements.txt
```

So the process is:

```text
Project
   ↓
Create .venv
   ↓
Activate .venv
   ↓
Read requirements.txt
   ↓
pip install -r requirements.txt
   ↓
Environment recreated
```

---

# 20. Why `.venv` Should Usually NOT Be Pushed to GitHub

The `.venv` directory can contain many files and installed packages.

It is usually unnecessary to upload the entire environment to GitHub.

Instead, upload:

```text
requirements.txt
```

and allow other developers to recreate the environment.

Therefore, `.gitignore` commonly contains:

```text
.venv/
```

Example:

```text
project/
│
├── .venv/              ← do not push
├── main.py
├── requirements.txt    ← push
└── .gitignore
```

---

# 21. `.gitignore` and Virtual Environments

A `.gitignore` file tells Git which files or directories should not be tracked.

For a Python project:

```gitignore
.venv/
__pycache__/
*.pyc
```

The important line for the virtual environment is:

```gitignore
.venv/
```

This prevents the virtual environment directory from being added to the Git repository.

---

# 22. Deactivating the Virtual Environment

When you are finished working with the environment:

```powershell
deactivate
```

The:

```text
(.venv)
```

will disappear from the terminal prompt.

For example:

Before:

```text
(.venv) PS C:\Users\sahul\Desktop\project>
```

After:

```text
PS C:\Users\sahul\Desktop\project>
```

---

# 23. Complete Virtual Environment Workflow

A typical Python project workflow is:

```powershell
mkdir my-project
cd my-project

python -m venv .venv

.venv\Scripts\Activate.ps1

pip install pandas

pip freeze > requirements.txt

deactivate
```

---

# 24. Working on an Existing Project

If the project already contains:

```text
requirements.txt
```

then:

```powershell
cd project
```

Create the environment:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
pip install -r requirements.txt
```

Now the project environment is ready.

---

# 25. Virtual Environment + Git + GitHub

These concepts work together.

A typical Python project can look like:

```text
project/
│
├── .venv/
│
├── main.py
│
├── requirements.txt
│
├── .gitignore
│
└── README.md
```

The workflow is:

```text
Create project
      ↓
python -m venv .venv
      ↓
Activate .venv
      ↓
Install packages
      ↓
Write Python code
      ↓
pip freeze > requirements.txt
      ↓
Add .venv/ to .gitignore
      ↓
git add .
      ↓
git commit
      ↓
git push
```

Another person can then clone the project:

```powershell
git clone <repository-url>
```

Enter the project:

```powershell
cd project
```

Create their own environment:

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Install the dependencies:

```powershell
pip install -r requirements.txt
```

They now have their own isolated environment.

---

# 26. Important Commands — Quick Reference

| Command | Purpose |
|---|---|
| `python -m venv .venv` | Create a virtual environment |
| `.venv\Scripts\Activate.ps1` | Activate on PowerShell |
| `.venv\Scripts\activate` | Activate on Windows CMD |
| `source .venv/bin/activate` | Activate on Linux/macOS |
| `deactivate` | Deactivate environment |
| `pip list` | Show installed packages |
| `pip show pandas` | Show information about pandas |
| `pip install pandas` | Install pandas |
| `pip uninstall pandas` | Uninstall pandas |
| `pip install --upgrade pandas` | Upgrade pandas |
| `pip freeze` | List installed packages with versions |
| `pip freeze > requirements.txt` | Save dependencies to requirements.txt |
| `pip install -r requirements.txt` | Install dependencies from requirements.txt |

---

# 27. The Most Important Mental Model

Remember this:

```text
                 PYTHON PROJECT
                       │
                       ↓
                Create .venv
                       │
                       ↓
                 Activate .venv
                       │
                       ↓
              Install dependencies
                       │
                       ↓
                  Write code
                       │
                       ↓
             pip freeze > requirements.txt
                       │
                       ↓
                .gitignore .venv/
                       │
                       ↓
                    GitHub
```

The key idea is:

```text
.venv
  ↓
Actual isolated environment

requirements.txt
  ↓
Description/list of dependencies needed
```

You generally **share `requirements.txt`, not `.venv`**.

---

# 28. Someone Else Can Recreate the Environment

If you share your project through GitHub, someone else can recreate the environment using:

```powershell
python -m venv .venv
```

Then activate it:

```powershell
.venv\Scripts\Activate.ps1
```

Then install the dependencies:

```powershell
pip install -r requirements.txt
```

They now have an environment containing the dependencies specified by the project.

---

# 29. Final Mental Model

Think of it this way:

```text
                 PROJECT
                    │
          ┌─────────┴─────────┐
          │                   │
       .venv            requirements.txt
          │                   │
          ↓                   ↓
   Actual environment    Dependency list
          │                   │
          ↓                   ↓
   Installed packages    Package names/versions
```

And with Git:

```text
                 GitHub
                    ↑
                    │
                  push
                    │
             Git repository
                    │
          ┌─────────┴─────────┐
          │                   │
 requirements.txt          .gitignore
          │                   │
       committed          .venv ignored
          │
          ↓
 Other developer
          │
          ↓
 python -m venv .venv
          │
          ↓
 pip install -r requirements.txt
          │
          ↓
 Same project dependencies
```

**Core idea to remember:**

> `.venv` is the isolated environment.  
> `pip` manages packages inside that environment.  
> `requirements.txt` records the dependencies.  
> `.gitignore` prevents `.venv` from being pushed to GitHub.  
> Another developer can create their own `.venv` and use `requirements.txt` to recreate the required dependencies.