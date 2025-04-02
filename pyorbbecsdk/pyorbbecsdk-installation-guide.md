# ✅ PyOrbbecSDK V2 Setup Guide (Windows)
Or you can just follow this:(https://orbbec.github.io/pyorbbecsdk/source/2_installation/installation.html)

Steps to get the Orbbec Python SDK v2 running with depth examples.

---

## 🔧 YOU NEED

| Tool                | Purpose                      |
|---------------------|------------------------------|
| **CMake** (≥ 3.15) | Building the C++ SDK         |
| **Visual Studio**   | Compiling C++ SDK + wrapper  |
| **Conda**           | Managing Python environment  |

---

## ✅ Confirm Tools Are Installed

Run this in PowerShell:
```bash
cmake --version
conda --version
```

---

## 🐍 Create Python Environment (Python 3.8)

```bash
conda create -n orbbec-dev python=3.8 -y
conda activate orbbec-dev
```

---

## 📅 Clone SDK v2 Branch

```bash
git clone https://github.com/orbbec/pyorbbecsdk.git
cd pyorbbecsdk
git checkout v2-main
```

---

## 📦 Install Python Dependencies

```bash
pip install -r examples/requirements.txt
```

---

## ⚙️ Build the Wrapper

```bash
mkdir build
cd build
cmake .. -A x64 -DOrbbecSDK_DIR="(YOUR pyorbbecsdk DIR)/pyorbbecsdk/sdk/lib/win_x64"
cmake --build . --config Release
cmake --install . --config Release --prefix ../install
```

---

## 💼 Install the SDK as a Python Package

Once installed to `install/lib/`, go back to the repo root and run:

```bash
cd ..
pip install .
```

This will register `pyorbbecsdk` as a proper Python package in your Conda environment so you can import it from anywhere.


## ▶️ Run an Example

From PowerShell:
```bash
python examples/depth.py
```

You should see a live depth stream from your Orbbec device 🎉

---

