# 🔥 Avatarify Colab (Dynamic Ngrok Auto-Refresh Edition)

This is a simplified, enhanced version of Avatarify powered by Google Colab and ngrok — designed for **easy setup, long sessions, and stability**.  
Perfect for using Avatarify with your **Mac client** + Colab worker combo, even without a GPU!

https://colab.research.google.com/drive/1dhVHUs289yLnQIvzS3PGs0Xjf-2-8esz?usp=sharing

---

## ✨ Features at a Glance

| Feature                               | This Notebook        | Official Avatarify |
|---------------------------------------|----------------------|--------------------|
| ✅ Auto-refreshing ngrok tunnels      | Yes                  | ❌ No              |
| ✅ Auto-patch for face_alignment bug  | Yes                  | ❌ No              |
| ✅ Worker auto-restart & monitoring   | Yes                  | ❌ No              |
| ✅ Supports webcam, OBS, or video     | Yes (`CAM_SOURCE`)   | ⚠️ Limited         |
| ✅ Clean UI with emoji log markers    | Yes                  | ❌ No              |
| ✅ Works with Mac + Colab setup       | Yes                  | ⚠️ Mostly Linux    |
| ✅ Beginner friendly with safe defaults | Yes                | ❌ No              |

---

## 🛠 What’s Included

- `avatarify_dynamic_ngrok.ipynb` — Enhanced Google Colab notebook
- Supports:
  - Webcam or virtual cam (OBS)
  - Pre-recorded video file (`test.mp4`)
- Run Avatarify in **real-time** using your **Mac as the client**
- Automatic ngrok management — **tunnels refresh every 60 mins**
- Includes a built-in fix for the `numpy.float32` → `torch.FloatTensor` error

---

## 🚀 How to Use

### 1. Clone or download this repo:
```bash
git clone https://github.com/DasolutionHub/Avatarify_Easy-Colab-Set-up.git
cd Avatarify_Easy-Colab-Set-up
