# 🐍 Python Commands & Setup Guide (Windows)

A comprehensive reference for Python development on Windows, covering environment setup, running scripts, package management, virtual environments, testing, and more.

---

## 🛠 Environment Setup (Windows)

| Command / Setting                         | Description                                     |
| ----------------------------------------- | ----------------------------------------------- |
| `python --version`                        | Check the installed Python version.             |
| `py --version`                            | Alternative to check Python version on Windows. |
| `where python`                            | Locate Python executable(s) on your system.     |
| **Set Python environment variable PATH:** |
> 1. Open **System Properties** → **Advanced** → **Environment Variables**.  
> 2. Under **System variables**, edit `Path` and add your Python install folder (e.g., `C:\Python39\`, and `C:\Python39\Scripts\`).  
> 3. Restart Command Prompt or PowerShell to apply changes. |
| `python`                                  | Start Python interactive shell.                               |
| `exit()` or `Ctrl+Z` + `Enter`            | Exit Python interactive shell.                                |

---

## ▶️ Running Python Programs

| Command                            | Description                                                |
| ---------------------------------- | ---------------------------------------------------------- |
| `python script.py`                 | Run a Python script file.                                  |
| `python -m module_name`            | Run a module as a script (e.g., `python -m http.server`).  |
| `py script.py`                     | Run script using Python launcher on Windows.               |
| `python -c "print('Hello World')"` | Run a one-liner Python command directly from command line. |

---

## 📦 Package Management with pip

| Command                              | Description                                           |
| ------------------------------------ | ----------------------------------------------------- |
| `pip --version`                      | Check pip version.                                    |
| `pip install package_name`           | Install a Python package from PyPI.                   |
| `pip uninstall package_name`         | Uninstall a package.                                  |
| `pip list`                           | List all installed packages.                          |
| `pip show package_name`              | Show detailed info about a specific package.          |
| `pip freeze > requirements.txt`      | Save installed packages and their versions to a file. |
| `pip install -r requirements.txt`    | Install packages listed in a requirements file.       |
| `pip install --upgrade package_name` | Upgrade an installed package to the latest version.   |

---

## 🌿 Virtual Environments

| Command                  | Description                                                          |
| ------------------------ | -------------------------------------------------------------------- |
| `python -m venv env`     | Create a virtual environment named `env`.                            |
| `.\env\Scripts\activate` | Activate virtual environment on Windows (PowerShell/Command Prompt). |
| `deactivate`             | Deactivate the virtual environment.                                  |
| `python -m venv --help`  | Display help for virtual environment options.                        |

---

## 🧪 Testing

| Command                             | Description                                                       |
| ----------------------------------- | ----------------------------------------------------------------- |
| `python -m unittest`                | Run all unit tests in the current directory.                      |
| `python -m unittest test_module.py` | Run specific test module.                                         |
| `pytest`                            | Run tests using Pytest framework (requires `pip install pytest`). |
| `pytest -v`                         | Run tests with verbose output.                                    |

---

## 🔧 Useful Python Commands

| Command                                             | Description                                               |
| --------------------------------------------------- | --------------------------------------------------------- |
| `python -m pip install --upgrade pip`               | Upgrade pip to the latest version.                        |
| `python -m site`                                    | Display site-specific directories used by Python.         |
| `python -m timeit -s "import math" "math.sqrt(25)"` | Time execution of small code snippets.                    |
| `python -m http.server`                             | Start a simple HTTP server serving the current directory. |
| `python -m cProfile script.py`                      | Profile a Python script’s performance.                    |

---

## 🧠 Tips for Python Development on Windows

- Always use virtual environments (`venv`) to isolate project dependencies.
- Use the Windows Python launcher `py` to easily manage multiple Python versions.
- Keep pip updated to avoid package installation issues.
- Use `requirements.txt` to manage and share project dependencies.
- Use `pytest` for more advanced testing capabilities than the built-in `unittest`.
- PowerShell and Command Prompt both work well; PowerShell offers advanced scripting.

---

## 🌐 External References

- [Official Python Documentation](https://docs.python.org/3/)
- [pip Documentation](https://pip.pypa.io/en/stable/)
- [venv — Virtual Environments](https://docs.python.org/3/library/venv.html)
- [pytest Documentation](https://docs.pytest.org/en/stable/)

---

## 📌 Recommended Basic Workflow (Windows)

### Create and activate a virtual environment:

```powershell
python -m venv env
.\env\Scripts\activate
