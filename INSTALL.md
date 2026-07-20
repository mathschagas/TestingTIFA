# Installing TestingTIFA (Windows)

This guide describes the exact environment used to successfully run the project.

**Repository**

```text
https://github.com/mathschagas/TestingTIFA
```

---

# Validated Environment

| Component | Version |
|-----------|---------|
| OS | Windows 11 |
| Python | 3.12 |
| pip | 24.0 |
| CUDA | Not required |
| Execution | CPU |

---

# 1. Clone the repository

```bash
git clone https://github.com/mathschagas/TestingTIFA.git
cd TestingTIFA
```

---

# 2. Check if Python 3.12 is installed

```bash
py -0p
```

You should see something similar to:

```text
-3.12  C:\Users\<USER>\AppData\Local\Programs\Python\Python312\python.exe
```

You can also verify it with:

```bash
py -3.12 --version
```

Expected:

```text
Python 3.12.x
```

---

# 3. Create the virtual environment

```bash
py -3.12 -m venv .venv
```

---

# 4. Activate the virtual environment

### Git Bash

```bash
source .venv/Scripts/activate
```

### PowerShell

```powershell
.\.venv\Scripts\Activate.ps1
```

### Command Prompt

```cmd
.venv\Scripts\activate.bat
```

---

# 5. Confirm the Python version

```bash
python --version
```

Expected:

```text
Python 3.12.x
```

---

# 6. Downgrade pip

This project depends on `pytorch-lightning==1.7.7`, whose metadata is rejected by recent versions of pip.

Install the validated version:

```bash
python -m pip install pip==24.0
```

Verify:

```bash
python -m pip --version
```

Expected:

```text
pip 24.0
```

---

# 7. Install dependencies

```bash
python -m pip install -r requirements-lock.txt
```

---

# 8. Install the project

```bash
python -m pip install -e .
```

---

# 9. Validate the installation

```bash
python -m pip check
```

Expected:

```text
No broken requirements found.
```

---

# 10. Run the benchmark

```bash
python meuteste.py
```

---

# First execution

During the first execution, ModelScope downloads the mPLUG Visual Question Answering model.

Approximate download size:

```text
2.78 GB
```

The download may take several minutes.

After that, the model will be loaded from the local cache:

```text
C:\Users\<USER>\.cache\modelscope\hub\models\damo\mplug_visual-question-answering_coco_large_en
```

---

# Expected output

The benchmark should finish with something similar to:

```text
Average TIFA is 0.8125
```

---

# Running again

After everything is installed:

```bash
cd TestingTIFA
source .venv/Scripts/activate

python meuteste.py
```

---

# Troubleshooting

## `pytorch-lightning==1.7.7` cannot be installed

Your pip version is too recent.

Install:

```bash
python -m pip install pip==24.0
```

and run the installation again.

---

## Wrong Python version

Delete the virtual environment and recreate it:

```bash
deactivate

rm -rf .venv

py -3.12 -m venv .venv
```