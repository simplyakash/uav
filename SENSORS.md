Radar vs LiDAR vs Camera — Drone Perception Guide

A clear, interview-ready comparison of the three core perception sensors.

🧠 1. High-Level Intuition
Camera → “What is it?” (semantics)

LiDAR → “Where is it?” (precise geometry) Point Cloud Representation P={(x,y,z,i)}

Radar → “How is it moving?” (velocity + robustness) R=f(range,velocity,angle)

📊 2. Comparison Table
| Feature             | Camera               | LiDAR             | Radar                    |
| ------------------- | -------------------- | ----------------- | ------------------------ |
| Output              | Images               | Point Cloud       | Range + Velocity + Angle |
| Data Type           | 2D (RGB)             | 3D (x, y, z)      | Sparse measurements      |
| Depth               | Indirect (ML/stereo) | Direct (accurate) | Direct (coarse)          |
| Velocity            | ❌                    | ❌                 | ✅ (Doppler)              |
| Range               | Medium               | Medium–High       | Very High                |
| Accuracy            | High (semantics)     | High (geometry)   | Medium                   |
| Weather Robustness  | ❌                    | ⚠️                | ✅                        |
| Lighting Dependency | High                 | Low               | None                     |
| Cost                | Low                  | High              | Medium                   |


📷 3. Camera
What it Provides
I ∈ R^(H × W × 3)

RGB images
Texture, color, semantics
Strengths
Object detection (cars, people, signs)
Semantic understanding
Low cost
Limitations
No direct depth
Sensitive to:
Lighting
Shadows
Weather
Example
Detects: “Car ahead”
But cannot reliably say: “Distance = 20 m”

📡 4. LiDAR
What it Provides
P = {(x, y, z, i)}

3D point cloud
Accurate spatial geometry
Strengths
Precise depth measurement
Works in low light
High spatial accuracy
Limitations
Expensive
Sparse at long distances
Performance drops in:
Rain
Fog
Example
Detects: “Object at (x=10, y=5, z=0)”
But doesn’t know: “What object is this?”

📡 5. Radar
What it Provides

R=f(range,velocity,angle)
Strengths
Measures velocity directly (Doppler effect)
Works in:
Fog
Rain
Dust
Long range
Limitations
Low resolution
Poor object shape
Hard to classify objects
Example
Detects: “Object at 50 m moving at -10 m/s”
But cannot say: “Car or pedestrian?”

🔄 6. Complementarity (Why We Fuse)
Sensor	Best At
Camera	Semantics
LiDAR	Geometry
Radar	Motion

👉 Together:

Camera → identifies object
LiDAR → gives exact position
Radar → gives velocity
🧪 7. Real Drone Example
Scenario: Drone tracking a moving car
Camera
Detects: “Car”
LiDAR
Position: (x, y, z)
Radar
Velocity: -5 m/s
Fusion Output
Object: Car
Position: precise 3D
Velocity: accurate motion

👉 Result: robust tracking system

⚖️ 8. Trade-offs
Accuracy vs Robustness
Camera → high semantic accuracy
LiDAR → high geometric accuracy
Radar → high robustness
Cost vs Performance
Camera → cheapest
LiDAR → most expensive
Radar → moderate
⚠️ 9. Failure Cases
Sensor	Failure Scenario
Camera	Night, glare
LiDAR	Heavy rain/fog
Radar	Close-range clutter
📌 10. Summary
Camera → understands what
LiDAR → understands where
Radar → understands how fast

👉 Sensor fusion combines all three for reliable perception.

💡 Interview Answer (Strong)

"Camera provides semantic understanding, LiDAR provides accurate 3D geometry, and radar provides robust velocity measurements. I fuse them to leverage complementary strengths—camera for classification, LiDAR for localization, and radar for motion—ensuring robustness across environments."
