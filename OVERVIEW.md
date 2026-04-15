🚁 Drone Perception & Multi-Sensor Fusion — README Guide
A structured overview for Drone Perception Engineer (Computer Vision + Sensor Fusion) interviews.

🛰️ 1. Drone System Overview
A drone (UAV) is a cyber-physical system that integrates sensing, computation, and control.
Core Loop
Sense→Perceive→Estimate→Plan→Control


🧩 2. System Architecture


Mission Planning


Perception (Computer Vision + Sensors)


State Estimation (Sensor Fusion)


Planning & Decision Making


Flight Control


Actuation (Motors)



🔧 3. Key Subsystems
3.1 Perception System


Extracts environment understanding


Tasks:


Object detection


Depth estimation


Visual SLAM / Visual Odometry





3.2 State Estimation
Estimates the drone's pose using sensor fusion.

State Vector

x=[x,y,z,vx,vy,vz,qw,qx,qy,qz,ba,bg]

x = [x, y, z, v_x, v_y, v_z, q_w, q_x, q_y, q_z, b_a, b_g]

x=[x,y,z,vx​,vy​,vz​,qw​,qx​,qy​,qz​,ba​,bg​]

$x, y, z$ → position

$v_x, v_y, v_z$ → velocity

$q_w, q_x, q_y, q_z$ → orientation (quaternion)

$b_a, b_g$ → IMU biases


3.3 Flight Controller
Stabilizes the drone using feedback control.

PID Control Law



u(t) = Kₚ e(t) + K_d (de(t)/dt) + Kᵢ ∫ e(t) dt

3.4 Planning & Navigation


Path planning: 

A*(Graph-based search using cost + heuristic), 

Dijkstra’s Algorithm (Special case  of A* gurantees shortest path)

RRT  (Rapidly-exploring Random Tree- Randomly sample space and build a tree)

MPC (Model Predictive Control -Optimize trajectory over time horizon)


Obstacle avoidance



3.5 Communication


Protocols: MAVLink, ROS2 DDS


Ground station communication



3.6 Power System


LiPo battery


Power distribution



3.7 Actuation


Motors


ESCs (Electronic Speed Controllers)


Propellers



📡 4. Sensors & Data Formats
4.1 Camera (RGB / Stereo)
Use Cases


Object detection


Semantic segmentation


Visual odometry


Data Representation

I∈RH×W×3I \in \mathbb{R}^{H \times W \times 3}I∈RH×W×3


$H$ = height


$W$ = width


3 channels (RGB)



4.2 LiDAR
Use Cases


3D mapping


Obstacle detection


Point Cloud Representation

P={(x,y,z,i)}

P = \{(x, y, z, i)\}
P={(x,y,z,i)}


$x, y, z$ → spatial coordinates


$i$ → intensity



4.3 Radar
Use Cases


Long-range detection


Robust in fog/rain


Representation
R=f(range,velocity,angle)R = f(\text{range}, \text{velocity}, \text{angle})R=f(range,velocity,angle)

4.4 IMU (Inertial Measurement Unit)
Measurements

a=(ax,ay,az),ω=(ωx,ωy,ωz)



$a$ → linear acceleration


$\omega$ → angular velocity



4.5 GPS
Data
(plat,plon,h)(p_{lat}, p_{lon}, h)(plat​,plon​,h)


Latitude, Longitude, Altitude



4.6 Barometer
Relation
h∝log(Pₐₜₘ)


Used for altitude estimation



4.7 Magnetometer
Data
m = (mₓ, mᵧ, m_z)

Used for heading estimation



🔄 5. Multi-Sensor Fusion
5.1 Why Fusion?


Camera → rich semantics, no direct depth


LiDAR → accurate depth, sparse


IMU → high frequency, drifts over time


Fusion combines strengths of all sensors.

5.2 Fusion Levels


Raw-Level Fusion


Combine raw sensor outputs




Feature-Level Fusion


Combine extracted features




Decision-Level Fusion


Combine outputs of models





5.3 Extended Kalman Filter (EKF)
Prediction Step
xk∣k−1=f(xk−1,uk)x_{k|k-1} = f(x_{k-1}, u_k)xk∣k−1​=f(xk−1​,uk​)
Update Step
xk=xk∣k−1+K(yk−h(xk∣k−1))x_k = x_{k|k-1} + K \left( y_k - h(x_{k|k-1}) \right)xk​=xk∣k−1​+K(yk​−h(xk∣k−1​))

5.4 Optimization-Based Fusion (Factor Graph)
min⁡x∑i∥zi−hi(x)∥2\min_x \sum_i \| z_i - h_i(x) \|^2xmin​i∑​∥zi​−hi​(x)∥2


Used in SLAM systems



🧠 6. Sensor Synchronization
Time Alignment

taligned=t+Δtt_{aligned} = t + \Delta ttaligned​=t+Δt

Methods


Hardware synchronization


Timestamp interpolation



🗂️ 7. Data Formats & Middleware
ROS / ROS2 Message Types
SensorMessage TypeCamerasensor_msgs/ImageLiDARsensor_msgs/PointCloud2IMUsensor_msgs/ImuGPSsensor_msgs/NavSatFix

Dataset Formats
Dataset TypeFormatImagesPNG / JPEGLiDARBIN / PCDLogsROS Bag (.bag)MetadataJSON / CSV

⚙️ 8. System Design Considerations
Latency
Ttotal=Tsensor+Tcompute+Tfusion  

T_{total} = T_{sensor} + T_{compute} + T_{fusion}   

Ttotal​=Tsensor​+Tcompute​+Tfusion​

Bandwidth


LiDAR → high data rate


Camera → high FPS



Compute Constraints


Edge devices (Jetson, Snapdragon)


GPU vs CPU trade-offs



Robustness


Sensor redundancy


Failure handling (e.g., GPS dropout)



🧪 9. Example Fusion Pipeline


IMU (200 Hz) → prediction


Camera (30 Hz) → visual odometry


LiDAR (10 Hz) → mapping


GPS (5 Hz) → global correction


Output


Pose:


(x,y,z,orientation)

🎯 10. Interview Talking Points


Trade-offs: accuracy vs latency


Sensor calibration:


Intrinsic parameters


Extrinsic transformation




Example Extrinsic Transform

TlidarcameraT^{camera}_{lidar}Tlidarcamera​


Sensor synchronization challenges


Failure cases:


IMU drift


GPS loss


Visual degradation





📌 11. Summary


Drone perception relies on multi-sensor fusion


Core sensors:

Camera

LiDAR

IMU

GPS

Fusion approaches:

EKF

Factor graph optimization

Deep learning





💡 Key Interview Answer Template

Use IMU for high-frequency prediction, fuse camera/LiDAR for relative pose estimation, and correct drift using GPS via EKF or factor graph optimization, ensuring accurate time synchronization and calibration.

