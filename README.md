🧠 Stable Diffusion WebUI on AMD (7900 XTX) — Step-by-Step Guide

This guide explains how to get Stable Diffusion WebUI (AUTOMATIC1111 version) working on an AMD GPU, specifically tested with the AMD Radeon RX 7900 XTX on Windows. It covers installation, common errors, and how to avoid CPU fallback.

✅ Requirements

Windows 10/11

AMD GPU with DirectML support (we used Radeon RX 7900 XTX)

Python 3.10.6

Git

Basic knowledge of command line

🛠️ 1. Install Python 3.10.6 (not higher)

Download from https://www.python.org/downloads/release/python-3106/

During installation:

✅ Check "Add Python to PATH"

✅ Choose custom install > make sure pip is included

📥 2. Clone AMD-Compatible WebUI

git clone https://github.com/lshqqytiger/stable-diffusion-webui-amdgpu.git
cd stable-diffusion-webui-amdgpu

🧩 3. Modify webui-user.bat

Open webui-user.bat and set the following:

set PYTHON=
set GIT=
set VENV_DIR=
set COMMANDLINE_ARGS=--skip-torch-cuda-test --no-half --use-directml
call webui.bat

💡 What these flags do:

--skip-torch-cuda-test — Avoids checking for CUDA (we're on AMD, CUDA is NVIDIA)

--no-half — Prevents half-precision issues

--use-directml — Enables DirectML backend (AMD-compatible)

▶️ 4. Run the WebUI

Double-click or run webui-user.bat.
If successful, you will see:

Running on local URL: http://127.0.0.1:7860

Open it in your browser. 🎉

🧱 5. Common Errors + Fixes

❌ AttributeError: module 'torch' has no attribute 'dml'

Fix:

pip install torch-directml

❌ AttributeError: module 'torch' has no attribute 'storage'

Fix: Downgrade PyTorch (optional, only if persistent)

pip uninstall torch
pip install torch==1.12

❌ RuntimeError: Input type (float) and bias type (struct c10::Half) should be the same

Fix: You already fixed this with --no-half

❌ Failed to install ZLUDA: 'NoneType' object is not subscriptable

Fix: ZLUDA is experimental — skip it and stick with --use-directml

🔥 Proof of GPU Acceleration

Use Task Manager > Performance tab > GPU

Under "Compute 0" and "VRAM usage", you should see activity while generating

If not, something went wrong — double check the flags and that torch-directml is installed

🙌 Final Tips

Don't update Python beyond 3.10.6

Always use the amdgpu fork, not the regular WebUI repo

Use VRAM-friendly flags if needed: --lowvram --opt-sub-quad-attention

❤️ Credits

This README was crafted after real-world testing with a 7900 XTX. Created by [ReuchMind](https://github.com/reuchmind)  .

Got it working? Share it! Fork the repo, add your tweaks, and help the next! 💪

