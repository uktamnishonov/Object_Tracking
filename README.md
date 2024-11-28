# Link to Video Explanation: https://youtu.be/SNuitLoSG4U


# **🎯 Object Tracking with OpenCV**

This project showcases **real-time object tracking** using OpenCV's state-of-the-art tracking algorithms. By default, it uses the **CSRT (Discriminative Correlation Filter with Channel and Spatial Reliability)** tracker for robust and accurate tracking, but other trackers are supported as well.

---

## 🚀 **Features**

- **Interactive Object Selection**: Select the object to track using your mouse.
- **Real-Time Tracking**: Monitor the selected object’s movement in a live video stream.
- **Multiple Tracker Support**:
  - `BOOSTING`, `MIL`, `KCF`, `TLD`, `MEDIANFLOW`, `GOTURN`, `MOSSE`, `CSRT`
- **CSRT by Default**: Highly accurate and robust tracker suitable for complex scenarios.

---

## 🧐 **Why CSRT?**

The **CSRT tracker** is chosen due to its superior performance in handling challenging scenarios such as:

1. **Accuracy**:
   - Can handle scale variations, rotation, and partial occlusions better than most other trackers.

2. **Robustness**:
   - Outperforms simpler trackers like `KCF` or `MOSSE` in complex environments.

3. **Balanced Trade-Off**:
   - While slightly slower than `KCF`, its precision makes it ideal for applications where accuracy is critical.

| Tracker     | Accuracy | Speed | Robustness | Use Cases                         |
|-------------|----------|-------|------------|-----------------------------------|
| BOOSTING    | Low      | Slow  | Low        | Simple cases, baseline tracking  |
| MIL         | Medium   | Medium| Low        | Moderate motion or occlusions    |
| KCF         | Medium   | Fast  | Medium     | Real-time tracking with less precision |
| TLD         | High     | Slow  | High       | Tracking and detecting lost targets |
| MEDIANFLOW  | Medium   | Slow  | Low        | Smooth motion, fails on large motions |
| GOTURN      | High     | Medium| High       | Requires pre-trained deep models |
| MOSSE       | Low      | Very Fast | Low     | Real-time tracking for simple cases |
| **CSRT**    | **High** | Medium| **High**   | Complex object tracking scenarios |

---

## 📋 **Code Explanation**

### **1. Initialization of the Tracker**
```python
tracker_types = ['BOOSTING', 'MIL', 'KCF', 'TLD', 'MEDIANFLOW', 'GOTURN', 'MOSSE', 'CSRT']
tracker_type = tracker_types[7]  # Choosing 'CSRT'
```
- A list of trackers is defined, and `CSRT` is chosen for its accuracy and robustness.

---

### **2. Creating the Tracker**
```python
if tracker_type == 'CSRT':
    tracker = cv2.TrackerCSRT_create()
```
- The chosen tracker is initialized using OpenCV's API. You can select other trackers like `BOOSTING` or `KCF` as needed.

---

### **3. Object Selection**
```python
bbox = cv2.selectROI("Select Object to Track", frame, fromCenter=False, showCrosshair=True)
```
- The user selects the object by drawing a bounding box interactively.

---

### **4. Tracker Initialization**
```python
tracker.init(frame, bbox)
```
- Initializes the tracker with the selected object in the first frame.

---

### **5. Real-Time Tracking**
```python
success, bbox = tracker.update(frame)
```
- Continuously updates the tracker’s bounding box as the object moves.
- If tracking is lost, the program notifies the user with "Tracking lost!".

---

### **6. Visualizing the Bounding Box**
```python
if success:
    x, y, w, h = [int(v) for v in bbox]
    cv2.rectangle(frame, (x, y), (x + w, y + h), (255, 0, 0), 2)
```
- Draws a bounding box around the tracked object for visualization.

---

### **7. Program Termination**
```python
if cv2.waitKey(1) & 0xFF == ord('q'):
    break
```
- Stops the tracking loop when the `q` key is pressed.

---

## 🛠️ **Setup**

### **Requirements**
- Python 3.6+
- OpenCV with contrib modules (`opencv-contrib-python`)

### **Installation**
1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/object-tracking.git
   cd object-tracking
   ```
2. Install the dependencies:
   ```bash
   pip install opencv-contrib-python
   ```

---

## 🚀 **Run the Project**

### **Run the Program**
```bash
python main.py
```
1. Select an object to track using your mouse.
2. Observe the bounding box tracking the object in real-time.
3. Press `q` to quit.

---

## 🎥 **Example Usage**

1. **Select an Object**:  
   ![Object Selection](images/select_object.gif)

2. **Track the Object**:  
   ![Object Tracking](images/tracking_demo.gif)

---

## ⚙️ **Customization**

### **Change the Tracker**
Modify the `tracker_type` variable in `main.py` to use a different tracker:
```python
tracker_type = tracker_types[1]  # Example: Use MIL tracker
```

### **Use a Video File**
Instead of a webcam, provide the path to a video file:
```python
track_object(video_source='path/to/video.mp4')
```

---

## 🔧 **Future Improvements**

1. **Reinitialization**:
   - Add an object detection model to reinitialize the tracker when tracking is lost.
2. **Multi-Object Tracking**:
   - Extend functionality to support tracking multiple objects.
3. **Performance Optimization**:
   - Use faster trackers like `MOSSE` for applications requiring ultra-low latency.

---

## 📖 **References**

- OpenCV Documentation: [Object Tracking](https://docs.opencv.org/master/dc/d6b/group__tracker.html)
- Tutorials: [Learn OpenCV](https://www.learnopencv.com/)

---

## 💡 **Contributing**

Contributions are welcome! Feel free to:
- Fork the repository.
- Submit a pull request with enhancements or bug fixes.

---

## 📝 **License**

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
