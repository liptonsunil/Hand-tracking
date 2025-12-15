# Hand-tracking
Virtual Boundary Hand Tracker
A real-time Computer Vision application that tracks hand proximity to a virtual object without using Deep Learning.

Overview:

This project was developed as a Proof of Concept (POC) for the Internship Assignment. The objective was to build a real-time hand tracking system that detects when a user approaches a virtual on-screen object and triggers a specific warning state.

The Challenge: 

Accurately track a hand and measure distance without using modern AI libraries like MediaPipe, OpenPose, or Cloud APIs.

The Solution: 

This project utilizes classical Computer Vision techniques—specifically HSV Color Segmentation and Contour Analysis—to achieve robust tracking on standard CPU hardware.

Features:

Real-Time Tracking:

Detects hand position at 30+ FPS using CPU only.

Dynamic State Logic:
        🟢 SAFE: Hand is at a comfortable distance.
        🟠 WARNING: Hand is approaching the boundary.
        🔴 DANGER: Hand has breached the virtual boundary.
Calibration System: 

Built-in UI Trackbars to adjust skin tone detection for different lighting conditions.

Visual Feedback:

Dynamic drawing of contours, tracking points, and distance lines.

How It Works:

Since we could not use AI pose detection, the pipeline follows these steps:

Color Space Conversion: 

The webcam feed is converted from BGR to HSV (Hue, Saturation, Value). This allows us to isolate skin color based on pigment (Hue) rather than brightness, making it resistant to shadows.

Masking & Morphology: 

A binary mask is created. We use Erosion and Dilation to remove noise and fill gaps in the detected hand shape.

Contour Detection:

OpenCV finds the boundaries of the white "hand blob" in the mask.

Proximity Logic:

The system calculates the Euclidean Distance from the center of the virtual object to the closest point on the hand's contour.State changes are triggered based on pixel distance thresholds.

Getting Started Prerequisites You need Python installed.
This project relies on two main libraries:

pip install opencv-python numpy

Running the AppRun the main Python script:python hand_tracker.py
(Note: Ensure your webcam is connected).

How to Use (Calibration)When you first run the app, you might see a black screen or a "NO HAND" status. You must calibrate it to your lighting.A window named "Mask Helper" will appear.Adjust the Trackbars (sliders) until your hand is white and the background is black:

Hue Min/Max: Defines the skin color (usually 0-20 for skin).
Sat Min: Increase to remove white walls/papers.
Val Min: Increase to remove shadows.

Once calibrated, interact with the circle in the center of the main window
Press 'q' to quit the application.

Project Structure├
── hand_tracker.py    # The main application logic
├── README.md          # Project documentation
└── requirements.txt   # Dependencies
