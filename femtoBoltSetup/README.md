# 3D Reconstruction with Femto Bolt Camera

This README outlines the full setup process for using the **Femto Bolt** camera in a Conda-based Python environment for 3D reconstruction tasks. It includes environment preparation, SDK setup, Python wrapper compilation, and verification with a test script.

---

## 1. Set Up Your Conda Environment

### 1.1 Install Conda
**Download & Install:**
- Download Miniconda from the [Miniconda Download Page](https://docs.conda.io/en/latest/miniconda.html) and run the installer.
- During installation, choose to add Conda to your PATH (or use the Anaconda Prompt).

### 1.2 Install Build Tools
Before building the Orbbec Python wrapper, install the required development tools:

#### Install CMake
- Download and install CMake from the [CMake Download page](https://cmake.org/download/).
- During installation, ensure **"Add CMake to the system PATH"** is selected.

#### Install Visual Studio Build Tools
- Download and install **Visual Studio Build Tools** (or **Visual Studio Community Edition**).
- During installation, select the **"Desktop development with C++"** workload.

### 1.3 Create and Activate the Environment
Open the Anaconda Prompt and run:

```cmd
conda create -n reconstruction_env python=3.10
conda activate reconstruction_env
```

### 1.4 Install Required Python Libraries
Install the necessary libraries using pip:

```cmd
pip install open3d numpy opencv-python matplotlib
```

### 1.5 Verify Python Library Installation
Launch Python and run the following command:

```cmd
python -c "import open3d as o3d; import numpy as np; import cv2; import matplotlib.pyplot as plt; print('All libraries imported successfully!')"
```

**Expected output:**
```
All libraries imported successfully!
```

---

## 2. Verify the Windows Orbbec SDK

### 2.1 Download and Extract the SDK
**Download:**
Download the Windows release ZIP file (e.g., `OrbbecSDK_C_C++_v1.10.16_20241021_5113dad11_win_x64_release.zip`).

**Extract:**
Extract it to a folder (e.g., `C:\OrbbecSDK_release`).

### 2.2 Run a Sample Executable
Navigate to the sample executables folder:

```cmd
cd "C:\OrbbecSDK_release\Example\bin"
```

List the directory contents:

```cmd
dir
```

Run a sample executable (for example, `HelloOrbbec.exe`):

```cmd
HelloOrbbec.exe
```

**Expected Output:**
The console should display SDK version information, device details (Femto Bolt detected, firmware, serial number, etc.).

---

## 3. Build and Install the Python Wrapper

### 3.1 Clone the Python Wrapper Repository
Clone the repository into your Documents folder:

```cmd
cd C:\Users\jomi\Documents
git clone https://github.com/orbbec/pyorbbecsdk.git
```

**Repository location:**
```
C:\Users\jomi\Documents\pyorbbecsdk
```

### 3.2 Configure and Build the Native Components
Open a Command Prompt (or Developer Command Prompt) and navigate to the repository:

```cmd
cd C:\Users\jomi\Documents\pyorbbecsdk
mkdir build
cd build
```

Get the pybind11 CMake directory:

```cmd
python -m pybind11 --cmakedir
```

Example output:
```
C:\Users\jomi\Desktop\PhD\programs\envs\reconstruction_env\lib\site-packages\pybind11\share\cmake\pybind11
```

Now run:

```cmd
cmake .. -G "Visual Studio 17 2022" -A x64 -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=../install -Dpybind11_DIR="C:\Users\jomi\Desktop\PhD\programs\envs\reconstruction_env\lib\site-packages\pybind11\share\cmake\pybind11"
```

### 3.3 Build and Install
Build the project and then install the artifacts:

```cmd
cmake --build . --config Release --target INSTALL
```

Verify that the directory:
```
C:\Users\jomi\Documents\pyorbbecsdk\install\lib
```
contains the expected native libraries.

### 3.4 Install the Python Wrapper
Return to the repository root:

```cmd
cd ..
```

Install the package in editable mode:

```cmd
pip install -e . --config-settings editable_mode=compat
```

### 3.5 Verify the Python Wrapper Installation
Test the installation by running:

```cmd
python -c "import pyorbbecsdk; print('Orbbec Python wrapper installed successfully!')"
```

**Expected Output:**
```
Orbbec Python wrapper installed successfully!
```

---

## 4. Testing an Example Python Script

### 4.1 Run a Provided Python Example
Navigate to the Python example folder in the wrapper repository:

```cmd
cd C:\Users\jomi\Documents\pyorbbecsdk\examples
```

List the contents and locate a suitable script (e.g., `device_info.py`).

Run the script:

```cmd
python device_info.py
```

**Expected Output:**
The output should show the SDK initialization info and details about the Femto Bolt: number of devices, name, firmware version, serial number, and connection type.

---

✅ You are now fully set up for capturing 3D data with the Femto Bolt using Python!
