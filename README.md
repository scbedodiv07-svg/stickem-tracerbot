# Stick 'Em Project Specifications

## Development Platform
I am developing on a Windows laptop. But I intend for the web app to be run from my Android phone.

## Robot Idea
I want to build a two-wheeled, computer vision-based line-tracing robot that:
1. Uses my Android phone's sensors (e.g. accelerometer) to tell what the robot's current forward orientation is
2. Uses the back camera of my Android phone to capture a live video feed
3. Uses computer vision to analyze this this live video feed so as to "see" what is on the ground just in front of it, including but not limited to:
    * Line Edges & Contours: The vision system extracts the physical boundaries (left and right edges) of the line to define its exact width
    * Centerline / Centroid: It calculates the mathematical center of the line, providing a target coordinate the robot must stay aligned with
    * Heading Angle Error: It compares the centerline of the path to the robot's current forward orientation, generating an "error value" that dictates how hard the robot needs to steer to stay on track
    * Path Curvature: By analyzing the trajectory of the line a few steps ahead, the computer predicts upcoming sharp turns or intersections, allowing the robot to adjust its speed dynamically
    * Intersections & Markers: The software detects specific visual cues (e.g., T-junctions, cross marks, or colored codes) that tell the robot to stop, turn, or branch off to a new path
4. Uses the information from Points 1 to 3 in order to adjust the direction of motion of the robot so that the robot follows the path of the line.

Note that:
1. My Android phone will be mounted on the robot, such that the front of the phone matches the front of the robot and the back camera of my phone is pointing downwards at the ground.
2. All directions and motions of the robot should be based on analysis of the data from the live video feed captured by my Android phone's camera and my phone's sensor readings (e.g. accelerometer).
3. The robot should travel at a constant speed as it follows the line.

## Web App Requirements
The web app should also display:
1. A mini view of the live video feed that is currently being captured by my Android phone's back camera.
2. A START/STOP button that starts or stops the run (i.e. robot starts/stops following the line when the button is pressed).
3. An arrow showing the current direction of travel of the robot: ⬆️ for going straight,  ⬅️ for turning left, ➡️ for turning right.
4. An arrow showing the predicted upcoming direction of travel of the robot: ⬆️ for going straight,  ⬅️ for turning left, ➡️ for turning right.
5. A live table with headers "Run Time (s)" and "Accelerometer X (m/s^2)", "Accelerometer Y (m/s^2)", "Accelerometer Z (m/s^2)".
6. A live graph that plots "Accelerometer X (m/s^2)", "Accelerometer Y (m/s^2)" and "Accelerometer Z (m/s^2)" as separate lines against "Run Time (s)".

## Wheel and Servo Information
* The left wheel is plugged into Servo Slot 1. The right wheel is plugged into Servo Slot 2.
* The servos are MG90S micro-servos. They take ~200 ms to swing fully and have asymmetric travel (one direction goes further than the other). Plan for jitter. Their useful PWM range is 1000 to 2000, with 1500 = neutral / centred. Real motion often only happens in `1300–1700`; the extremes can stall.

## More Information on Line Tracing
I need the robot/app to accommodate for two line-tracing modes:
1. A dark black tape on a light-coloured floor (white, ivory, beige or light grey).
2. A white tape on a dark-coloured floor (black, dark grey).

The web app should include a button for switching between the two line-tracing modes.
