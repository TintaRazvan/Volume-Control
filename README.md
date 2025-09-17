# 🎛️ Volume Control - Hand Gesture Recognition

An intelligent volume control system that uses hand gesture recognition through webcam to adjust system volume in real-time.

![Python](https://img.shields.io/badge/python-v3.12+-blue.svg)
![OpenCV](https://img.shields.io/badge/opencv-4.x-green.svg)
![MediaPipe](https://img.shields.io/badge/mediapipe-latest-orange.svg)
![Platform](https://img.shields.io/badge/platform-windows%20%7C%20mac%20%7C%20linux-lightgrey.svg)

## 📋 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Demo](#-demo)
- [System Requirements](#-system-requirements)
- [Installation](#-installation)
- [Usage](#-usage)
- [How It Works](#-how-it-works)
- [Configurable Parameters](#-configurable-parameters)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

## 🎯 About

**Volume Control** is an innovative Python application that enables hands-free system volume control through simple hand gestures detected via webcam. Using advanced computer vision and machine learning technologies, the application provides an intuitive hands-free experience for volume adjustment.

### 🌟 Project Motivation

This project was developed to provide:
- An intuitive alternative to traditional volume control methods
- An accessibility-friendly solution for people with reduced mobility
- A practical demonstration of MediaPipe and OpenCV capabilities
- A foundation for gesture-based human-computer interaction

## ✨ Features

### 🔍 Core Functionality
- **Real-Time Detection**: Instant hand gesture recognition
- **Intuitive Control**: Volume adjusts based on distance between thumb and index finger
- **Visual Feedback**: Display of landmarks and connecting lines
- **Optimized Performance**: Efficient processing for smooth experience
- **Cross-Platform**: Compatible with Windows, macOS, and Linux
- **Lightweight**: Minimal system resource usage

### 🎮 Supported Gestures
- **👆 Large Distance**: Increases volume (fingers spread apart)
- **🤏 Small Distance**: Decreases volume (fingers close together)
- **📊 Visual Feedback**: Green line connecting fingers for visual control
- **🎯 Landmark Detection**: Precise finger tip tracking

## 🎬 Demo

```
🎥 To see the application in action:
1. Run the application
2. Position your hand in front of the camera
3. Vary the distance between your thumb and index finger
4. Watch the volume change in real-time
```

### Expected Behavior
- **Distance > 50 pixels**: Volume Up
- **Distance ≤ 50 pixels**: Volume Down
- **Yellow Circle**: Index finger (landmark 8)
- **Red Circle**: Thumb (landmark 4)
- **Green Line**: Connection between control points

## 💻 System Requirements

### Hardware Requirements
- **Webcam**: Any OpenCV-compatible camera
- **RAM**: Minimum 4GB (8GB+ recommended)
- **CPU**: Intel i3/AMD Ryzen 3 or higher
- **OS**: Windows 10+, macOS 10.14+, Linux Ubuntu 18.04+

### Software Requirements
- **Python**: Version 3.12 or newer
- **Pip**: For dependency installation
- **Camera Permissions**: Access to webcam

## 🚀 Installation

### Method 1: Clone Repository

```bash
# Clone the project
git clone https://github.com/yourusername/volume-control.git
cd volume-control

# Create virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Method 2: Manual Installation

```bash
# Install required packages
pip install opencv-python
pip install mediapipe
pip install pyautogui
```

### 📋 requirements.txt

```txt
opencv-python>=4.8.0
mediapipe>=0.10.0
pyautogui>=0.9.54
numpy>=1.24.0
```

## 🎯 Usage

### Basic Usage

```bash
# Run the application
python volume_control.py
```

### Controls
- **ESC Key**: Exit the application
- **Hand Gestures**: Control volume by adjusting finger distance
- **Camera View**: Monitor hand detection in real-time

### Step-by-Step Guide

1. **Launch Application**
   ```bash
   python volume_control.py
   ```

2. **Position Your Hand**
   - Hold your hand 1-2 feet from the camera
   - Ensure good lighting conditions
   - Keep background relatively simple

3. **Control Volume**
   - Spread thumb and index finger apart → Volume Up
   - Bring thumb and index finger together → Volume Down

4. **Exit**
   - Press ESC key to quit the application

## 🔧 How It Works

### Technical Overview

The application uses a sophisticated computer vision pipeline:

1. **Video Capture**: OpenCV captures frames from webcam
2. **Hand Detection**: MediaPipe identifies hand landmarks
3. **Gesture Analysis**: Calculates distance between specific landmarks
4. **Volume Control**: PyAutoGUI sends volume commands to system
5. **Visual Feedback**: Real-time display of detection results

### Key Components

#### Hand Landmark Detection
```python
# MediaPipe hand detection
my_hands = mp.solutions.hands.Hands()
output = my_hands.process(rgb_image)
```

#### Distance Calculation
```python
# Calculate distance between thumb and index finger
dist = ((x2-x1)**2 + (y2-y1)**2)**(0.5) // 4
```

#### Volume Control Logic
```python
if dist > 50:
    pyautogui.press('volumeup')
else:
    pyautogui.press('volumedown')
```

### Landmark Points Used
- **Landmark 4**: Thumb tip
- **Landmark 8**: Index finger tip

## ⚙️ Configurable Parameters

You can modify these parameters in the code:

| Parameter | Default | Description |
|-----------|---------|-------------|
| `threshold` | 50 | Distance threshold for volume control |
| `circle_radius` | 8 | Size of landmark circles |
| `line_thickness` | 3 | Thickness of connecting line |
| `camera_index` | 0 | Webcam device index |

### Example Customization

```python
# Adjust sensitivity
VOLUME_THRESHOLD = 75  # Increase for less sensitivity

# Change visual feedback
CIRCLE_RADIUS = 12     # Larger circles
LINE_THICKNESS = 5     # Thicker line

# Different colors
THUMB_COLOR = (255, 0, 0)      # Blue thumb
INDEX_COLOR = (0, 255, 255)    # Yellow index
LINE_COLOR = (255, 255, 0)     # Cyan line
```

## 🐛 Troubleshooting

### Common Issues

#### Camera Not Detected
```bash
# Check available cameras
python -c "import cv2; print(cv2.VideoCapture(0).isOpened())"
```

#### Poor Hand Detection
- Ensure adequate lighting
- Keep hand within camera frame
- Avoid cluttered backgrounds
- Clean camera lens

#### Volume Not Changing
- Check system permissions for automation
- Verify PyAutoGUI compatibility with your OS
- Test with other applications

#### Performance Issues
- Close unnecessary applications
- Lower camera resolution
- Optimize lighting conditions

### Platform-Specific Notes

#### Windows
- May require administrator privileges for volume control
- Windows Defender might flag PyAutoGUI

#### macOS
- Grant accessibility permissions in System Preferences
- Camera permissions required

#### Linux
- Install additional dependencies: `sudo apt-get install python3-tk`
- Check audio system compatibility

## 🤝 Contributing

We welcome contributions! Here's how you can help:

### Development Setup

```bash
# Fork the repository
git clone https://github.com/yourusername/volume-control.git
cd volume-control

# Create feature branch
git checkout -b feature/your-feature-name

# Make changes and test
python volume_control.py

# Commit changes
git add .
git commit -m "Add: your feature description"

# Push to branch
git push origin feature/your-feature-name
```

### Contribution Guidelines

1. **Code Style**: Follow PEP 8 standards
2. **Testing**: Test on multiple platforms
3. **Documentation**: Update README for new features
4. **Issues**: Use GitHub issues for bug reports

### Areas for Improvement

- [ ] Add gesture customization
- [ ] Implement gesture recording
- [ ] Support for multiple hands
- [ ] GUI configuration panel
- [ ] Gesture training mode
- [ ] Volume level display
- [ ] Custom key bindings

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2024 Volume Control Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions...
```

## 📞 Contact

- **Author**: Your Name
- **Email**: your.email@example.com
- **GitHub**: [@yourusername](https://github.com/yourusername)
- **LinkedIn**: [Your LinkedIn](https://linkedin.com/in/yourprofile)

## 🙏 Acknowledgments

- **MediaPipe Team**: For the excellent hand tracking solution
- **OpenCV Community**: For computer vision tools
- **PyAutoGUI**: For system automation capabilities
- **Python Community**: For the amazing ecosystem

## 📊 Project Stats

![GitHub stars](https://img.shields.io/github/stars/yourusername/volume-control)
![GitHub forks](https://img.shields.io/github/forks/yourusername/volume-control)
![GitHub issues](https://img.shields.io/github/issues/yourusername/volume-control)
![GitHub license](https://img.shields.io/github/license/yourusername/volume-control)

---

⭐ **If this project helped you, please give it a star!** ⭐
