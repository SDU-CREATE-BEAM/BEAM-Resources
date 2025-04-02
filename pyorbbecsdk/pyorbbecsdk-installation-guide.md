# ✅ PyOrbbecSDK V2 Setup Guide (Windows)

Steps to get the Orbbec Python SDK v2 running with depth examples.

---

## 🔧 YOU NEED

| Tool                | Purpose                      |
|---------------------|------------------------------|
| **CMake** (>= 3.15) | Building the C++ SDK         |
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

## 📥 Clone SDK v2 Branch

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
```

---

## 📂 Copy Build Output

From inside `pyorbbecsdk/build`, copy files into the main SDK directory:

```bash
copy Release\\*.pyd ..
copy ..\\sdk\\lib\\win_x64\\*.dll ..
```

Your folder structure should now include:
- `pyorbbecsdk.cp38-win_amd64.pyd`
- `OrbbecSDK.dll`

---

## 🧠 OPTIONAL: Set PYTHONPATH Permanently

1. Press `Win + S` → search for **Edit environment variables**
2. Click **Environment Variables**
3. Under **System Variables**, click **New**
   - **Name:** `PYTHONPATH`
   - **Value:** `C:\\path\\to\\pyorbbecsdk`

Now Python can find the `.pyd` module automatically.

---

## ▶️ Run an Example

From PowerShell:
```bash
cd C:\\path\\to\\pyorbbecsdk
python examples/depth.py
```

You should see a live depth stream from your Orbbec device 🎉

---