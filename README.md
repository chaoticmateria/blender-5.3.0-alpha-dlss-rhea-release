# Blender Rhea Release - Custom Build with Full CUDA, OptiX & DLSS 3.5 Support

Welcome to the **Blender Rhea Release** repository! This is a custom Windows build of Blender compiled specifically to ensure maximum compatibility and performance with NVIDIA GPUs. It comes pre-compiled with full support for **CUDA**, **OptiX**, and **DLSS 3.5 (Ray Reconstruction)** right out of the box.

## 📥 Download Pre-compiled Binary
If you just want to use this custom build without compiling it yourself, you can download the ready-to-use `.zip` file from the **Releases** tab.
1. Download the latest `Blender-Rhea-Release-Win64.zip`.
2. Extract the folder to your preferred location.
3. Run `blender.exe` and enjoy!

---

## 🛠️ How to Build It Yourself (For Developers)

If you want to compile this custom build from the source code, follow the detailed instructions below. This guide assumes you are on **Windows 11/10**.

### 1. Prerequisites & SDKs
Before you begin, you must install the following developer tools and SDKs:
- **Visual Studio 2022 Community** (Make sure to install the "Desktop development with C++" workload).
- **Git** for Windows.
- **CMake** (Ensure it is added to your system PATH).
- **[CUDA Toolkit](https://developer.nvidia.com/cuda-downloads)** (Required for rendering CUDA kernels).
- **[OptiX SDK](https://developer.nvidia.com/designworks/optix/download)** (Required for OptiX hardware raytracing).
- **[NVIDIA Streamline SDK](https://github.com/NVIDIAGameWorks/Streamline)** (Required for DLSS 3.5 support).

### 2. Download the Source Code
Open your terminal (PowerShell) and clone the official Blender repository along with its precompiled libraries:
```powershell
mkdir D:\blender-git
cd D:\blender-git
git clone https://projects.blender.org/blender/blender.git
```
Next, download the required precompiled libraries for Windows:
```powershell
cd D:\blender-git\blender
make update
```

### 3. Setup Environment Variables
Before running the build script, you must tell the compiler where your NVIDIA SDKs are located. Open PowerShell and set the following variables (adjust the paths if you installed them elsewhere):

```powershell
$env:CUDA_PATH = "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.9"
$env:CUDA_TOOLKIT_ROOT_DIR = "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.9"
$env:OPTIX_ROOT_DIR = "C:\ProgramData\NVIDIA Corporation\OptiX SDK 9.1.0"
$env:DLSS_SDK_ROOT = "D:\blender-git\streamline-sdk-v2.10.3\external\ngx-sdk"
$env:PATH += ";C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.9\bin"
```

### 4. Compile Blender (Ninja Generator)
Once the environment is properly configured, navigate to the `blender` folder and start the build process using the `ninja` build system for maximum speed:

```powershell
cd D:\blender-git\blender
.\make.bat release ninja
```

Wait for the compilation to finish (this can take anywhere from 45 minutes to 2 hours depending on your CPU). 

### 5. Run Your Custom Build
Once the build is complete, you will find your compiled executable in the following directory:
`D:\blender-git\build_windows_Release_x64_vc17_Release\bin\blender.exe`

---

## 📜 License
This custom build respects and falls under the **GNU General Public License v3.0 (GPLv3)**, inheriting the same license as the official Blender Foundation release. The NVIDIA Streamline SDK and DLSS libraries are dynamically loaded and follow NVIDIA's EULA.
