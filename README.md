# AI-Aimbot

# AI-Powered Auto-Aiming System with YOLO v8 Object Detection for FPS Games

## 🚀 Quick Start

```bash
# 1. Install dependencies (one-time)
pip install -r requirements.txt

# 2. Launch the program
python launcher.py

# 3. Hotkey to enable/disable
F6 = Toggle Tracking
```

## 📁 Folder Structure

```
.
├── launcher.py                 # 🎮 Start menu (START HERE!)
├── main.py                     # 💻 CLI main program
├── gui_main.py                 # 🎨 GUI alternative
├── config.py                   # ⚙️ Configuration options
├── config_presets.py           # 📋 Preset configurations
├── requirements.txt            # 📦 Python dependencies
│
├── core/                       # 🧠 Core modules
│   ├── capture.py              # 📸 Screen capture (dxcam)
│   ├── detector.py             # 🤖 YOLO object detection
│   ├── selector.py             # 🎯 Target selection logic
│   └── mouse_controller.py     # 🖱️ Mouse control & smoothing
│
├── gui/                        # 🎨 Graphical interface
│   └── main_window.py          # PyQt5 GUI
│
├── utils/                      # 🛠️ Utility functions
│   ├── hotkey_manager.py       # ⌨️ Hotkey system (F6)
│   ├── fps_counter.py          # 📊 Performance monitoring
│   └── window_selector.py      # 🪟 Window selection
│
├── models/                     # 🤖 AI models (YOLO)
│   ├── yolov8n.pt              # Fast (60+ FPS)
│   ├── yolov8s.pt              # Balanced ← CURRENTLY USED
│   └── yolov8m.pt              # Accurate (up to 30 FPS)
│
└── README.md                   # This file
```

## 📄 What Does Each File Do?

**Main Programs**
- `launcher.py` — Menu to launch CLI, GUI, or Window Selector
- `main.py` — Core program (TrackingSystem class + configuration)
- `gui_main.py` — Graphical interface with live preview

**Configuration**
- `config.py` — All adjustable parameters (model, GPU, auto-shoot, etc.)
- `config_presets.py` — Preset configs (CSGO, Valorant, Balanced, etc.)
- `requirements.txt` — Python packages (torch, ultralytics, opencv, etc.)

**Core Modules (the magic)**
- `capture.py` — Takes screenshots (60–120 FPS possible)
- `detector.py` — Detects players using YOLO (AI model)
- `selector.py` — Selects the best target (closest to crosshair)
- `mouse_controller.py` — Moves mouse smoothly + auto-click

**Utilities**
- `hotkey_manager.py` — F6 toggle listener
- `fps_counter.py` — Displays performance (FPS) in console
- `window_selector.py` — Window list for tracking

## ⚙️ Configuration

All settings are in `config.py` (`main.py` → `main()` function):

```python
# GPU (IMPORTANT!)
device="dml"                    # AMD RX 6750XT → "dml"
                                # NVIDIA → "cuda"
                                # CPU → "cpu"

# Model
model_path="models/yolov8s.pt"  # n=fast, s=balanced, m=accurate

# Region (optimized for 1920x1080)
capture_region=(0, 0, 1920, 950)  # Upper area only (no weapon)

# Tracking
conf_threshold=0.5              # 0.0–1.0 (higher = more accurate)
smoothing_alpha=0.2             # 0.0=smooth, 1.0=jittery

# Auto-Shoot
auto_shoot=True
shoot_threshold_px=30           # Only shoot if close enough
shoot_cooldown_ms=80.0          # Minimum time between shots
```

## 🎮 Usage

**Option 1: CLI (Default)**
```bash
python launcher.py
# Choose: 1 (CLI Mode)
```
- Fast and lightweight
- F6 to activate
- Ctrl+C to quit

**Option 2: GUI**
```bash
python launcher.py
# Choose: 2 (GUI Mode)
```
- Preview + live stats
- All parameters adjustable
- See detections in real time

**Option 3: Window Selector**
```bash
python launcher.py
# Choose: 3 (Window Selector)
```
- Window tracking
- Track only the game window

## 🔫 Auto-Shoot Tuning

**Too aggressive? (shoots everywhere)**
```python
shoot_threshold_px=20   # Was 30 (lower = less frequent)
conf_threshold=0.6      # Was 0.5 (more filtering)
```

**Too weak? (not shooting enough)**
```python
shoot_threshold_px=40   # Was 30 (higher = more frequent)
conf_threshold=0.4      # Was 0.5 (less filtering)
```

## 📊 Expected FPS

With RX 6750XT + yolov8s + 1920×1080:

| Component | Performance |
|---|---|
| Capture FPS | 120 FPS |
| Inference FPS | 80–120 FPS |
| Total System | 80+ FPS realistic |

## 🔧 Common Issues

**"Module not found"**
```bash
pip install -r requirements.txt
```

**"GPU not recognized"**
```python
# In config.py: device="cpu"
```

**"Hotkey not working"**
- Run as Administrator
- Or use Ctrl+C to quit

**"Shoots everywhere"** → See "Auto-Shoot Tuning" above

## 🎯 Performance Tips

**If too slow:**
- Use a smaller model: `yolov8n.pt`
- Lower FPS target: `target_fps=60`
- Reduce capture region (partial screen)

**If latency is high:**
- Check GPU mode: `device="dml"`
- Increase smoothing: `smoothing_alpha=0.3`

## 💡 Hotkeys

| Key | Function |
|---|---|
| F6 | Toggle tracking on/off |
| Ctrl+C | Quit program |

## 📦 Installation

```bash
# Install dependencies (one-time)
pip install -r requirements.txt

# YOLO model downloads automatically on first run
# If not, download manually with:
python -c "from ultralytics import YOLO; YOLO('yolov8s.pt')"
```

## ⚠️ Disclaimer

- For educational purposes & testing only
- Do not use in competitive online games (VAC ban risk)
- Respect local laws and terms of service
- Use F6 to quickly disable

Good luck! 🎯