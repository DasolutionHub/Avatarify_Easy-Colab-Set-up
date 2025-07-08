<p align="center">
  <img src="https://github.com/dasolutionhub/avatarify-colab-mac-guide/raw/main/Avatarify Mac Client.png" alt="Avatarify Colab Banner" />
</p>

# 🔥 Avatarify Colab (Mac Client Edition by Dasolutionhub)



This is a simplified, enhanced version of Avatarify powered by Google Colab and ngrok — designed for **easy setup, long sessions, and stability**.\
Perfect for using Avatarify with your **Mac client** + Colab worker combo, even without a GPU!

[![Open In Colab](https://colab.research.google.com/drive/1SEQsNRGwgtbBBD2CASJ07GMrPAYg4YIy?usp=sharing)

---

## ✨ Features at a Glance

| Feature                                | This Notebook      | Official Avatarify |
| -------------------------------------- | ------------------ | ------------------ |
| ✅ Auto-refreshing ngrok tunnels        | Yes                | ❌ No               |
| ✅ Auto-patch for face\_alignment bug   | Yes                | ❌ No               |
| ✅ Worker auto-restart & monitoring     | Yes                | ❌ No               |
| ✅ Supports webcam, OBS, or video       | Yes (`CAM_SOURCE`) | ⚠️ Limited         |
| ✅ Clean UI with emoji log markers      | Yes                | ❌ No               |
| ✅ Works with Mac + Colab setup         | Yes                | ⚠️ Mostly Linux    |
| ✅ Beginner friendly with safe defaults | Yes                | ❌ No               |

---

## 🚀 One-Click Colab Setup

⬆️ Open the notebook\
⬆️ Follow the instructions\
⬆️ Copy the terminal command shown into your Mac

---

## 💻 How to Install and Run Avatarify on Your Mac (Client Side)

Follow this exact setup to prepare your Mac to work as the client for the Colab-powered Avatarify worker.

### 📆 1. Remove any old Avatarify installations

```bash
conda deactivate
conda env remove -n avatarify -y
rm -rf ~/avatarify-python
```

---

### ↺ 2. Clone the official Avatarify repo

```bash
git clone https://github.com/alievk/avatarify-python.git
cd avatarify-python
```

---

### 🐍 3. Create a fresh conda environment with Python 3.7

```bash
conda create -n avatarify python=3.7 -y
conda activate avatarify
```

---

### ⚖️ 4. Install fixed versions of core dependencies

```bash
pip install numpy==1.15.0 PyYAML==5.1 requests==2.28.2 msgpack-numpy==0.4.5 pyzmq==19.0.0 opencv-python==3.4.5.20
```

---

### ✅ 5. Verify installations

```bash
pip list | egrep "numpy|PyYAML|requests|msgpack|pyzmq|opencv"
```

Expected output:

```
numpy             1.15.0  
opencv-python     3.4.5.20  
msgpack-numpy     0.4.5  
pyzmq             19.0.0  
PyYAML            5.1  
requests          2.28.2
```

Then run:

```bash
python -c "import numpy, cv2, yaml, requests; print('Success!')"
```

---

### 🛠 6. Create a fixed `run_mac.sh` script

```bash
cat << 'EOF' > run_mac.sh
#!/usr/bin/env bash

kill -9 $(ps aux | grep 'afy/cam_fomm.py' | awk '{print $2}') 2> /dev/null

source $(conda info --base)/etc/profile.d/conda.sh
conda activate avatarify

export PYOPENGL_PLATFORM="osmesa"

CONFIG=fomm/config/vox-adv-256.yaml
CKPT=vox-adv-cpk.pth.tar

export PYTHONPATH=$PYTHONPATH:$(pwd):$(pwd)/fomm

python afy/cam_fomm.py --config "$CONFIG" --checkpoint "$CKPT" --relative --adapt_scale --no-pad $@
EOF

chmod +x run_mac.sh
```

---

### 📥 7. Download model weights and test video

```bash
curl -OL https://github.com/alievk/avatarify/releases/download/models/vox-adv-cpk.pth.tar
curl -OL https://github.com/alievk/avatarify/raw/master/samples/test.mp4
```

---

### ✅ 8. Verify that it runs

```bash
./run_mac.sh --help
```

This should print the available command-line options for Avatarify.

---

## 🩺 Optional (but recommended): Fix the `face_alignment` error

If you later see a `TypeError: can't assign a numpy.float32 to a torch.FloatTensor` — apply this patch.

### Step-by-step:

```bash
nano /Users/$(whoami)/miniconda3/envs/avatarify/lib/python3.7/site-packages/face_alignment/utils.py
```

Find:

```python
t[0, 0] = resolution / h
t[1, 1] = resolution / h
```

Replace with:

```python
t[0, 0] = float(resolution / h)
t[1, 1] = float(resolution / h)
```

Then:

- Press `Ctrl + O`, `Enter` to save
- Press `Ctrl + X` to exit nano

---

## 📽️ Avatarify Client Command Example (on Mac)

Once setup is complete, paste the Colab-generated command:

```bash
CAM_SOURCE=test.mp4 \
  ./run_mac.sh --is-client \
    --in-addr tcp://X.tcp.ngrok.io:PORT1 \
    --out-addr tcp://Y.tcp.ngrok.io:PORT2
```

Replace the ngrok addresses with those shown in Colab.

Use:

- `CAM_SOURCE=0` for webcam
- `CAM_SOURCE=1` for OBS virtual cam
- `CAM_SOURCE=test.mp4` for pre-recorded video

---

## 🔍 Add Your Own Avatar

1. Place your image (PNG/JPG) into the `avatars/` folder
2. Use the `Tab` key while Avatarify is running to select it

Pro tip: Use a clear, front-facing photo for best results.

---

## 😳 Still Need Help?

Feel free to open an issue or chat on Telegram at [@dasolutionhub]!

---

**Built with ❤️ by Dasolutionhub to help anyone get Avatarify running without stress.**

