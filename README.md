# 🏯 AI Temple Crowd Tracking System

A multi-agent Computer Vision system designed to monitor occupancy levels in real-time and trigger automated security responses using YOLOv8.

---

## 🌟 Project Overview
This system provides an automated solution for public safety in high-traffic areas like temples, mosques, or public events. By leveraging the **YOLOv8** deep learning model, the system identifies the number of people in a camera feed and delegates tasks across three specialized AI "Agents" to manage data, analyze risk, and execute security protocols.



## 🤖 Agentic Architecture
The system is built on a modular, agent-based design. Each class acts as a specialized agent:

1. **The Observer (`ObserverAgent`):** - **Role:** The Eyes.
   - **Function:** Captures raw video frames and runs the YOLOv8 Nano model.
   - **Specialization:** It is filtered to only "see" Class 0 (Persons), ignoring background noise, vehicles, or animals.

2. **The Analyst (`AnalystAgent`):** - **Role:** The Brain.
   - **Function:** Evaluates the count provided by the Observer. 
   - **Logic:** It determines if the crowd density is `NORMAL`, `WARNING` (80% capacity), or `CRITICAL` (100%+ capacity).

3. **The Warden (`WardenAgent`):** - **Role:** The Action.
   - **Function:** Executes defense and alert protocols.
   - **Actions:** It writes to a permanent log file, prints red-text alerts to the console, and triggers a hardware system beep for immediate attention.



## 🛠 Technical Configuration Explained
To customize the system for your specific environment, you can modify the parameters within the script. Here is why they are configured this way:

| Configuration | Location | Default | Purpose |
| :--- | :--- | :--- | :--- |
| **Threshold** | `AnalystAgent(threshold=10)` | `10` | The maximum safe capacity. Adjust this based on the square footage of your venue. |
| **Model Version** | `YOLO('yolov8n.pt')` | `yolov8n` | "Nano" is used because it is the fastest version, essential for real-time processing on standard laptops. |
| **Detection Class** | `classes=[0]` | `0` | COCO Dataset index for "Person". Ensures the system doesn't count chairs or statues as people. |
| **Warning Buffer** | `threshold * 0.8` | `80%` | Provides a "Yellow Alert" phase before the situation becomes critical. |

## ✨ Features
* **Real-time Detection:** Optimized for low-latency performance.
* **Modular Design:** Easy to swap detection models or alert mechanisms without breaking core logic.
* **Visual Feedback:** Dynamic UI that changes color (Green to Red) based on threat levels.
* **Automated Logging:** Saves all security breaches with timestamps in `temple_security_logs.txt`.

---

## ⚙️ Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/yourusername/temple-crowd-tracking.git](https://github.com/yourusername/temple-crowd-tracking.git)
   cd temple-crowd-tracking
Install Dependencies:

Bash

pip install opencv-python ultralytics
Run the System:

Bash

python main.py
🚀 Usage Instructions
Starting: Once the script runs, your default webcam will activate.

Monitoring: The screen will show bounding boxes around people and a live "People Count."

Alerts: If the count exceeds your threshold, the screen text turns Red, a beep will sound, and a log entry is created.

Exiting: Press the q key on your keyboard to safely close the video stream.

📜 License
This project is licensed under the MIT License.

🤝 Contributing
Contributions are welcome! If you'd like to add SMS alerts via Twilio or Cloud Logging, please open a Pull Request.
