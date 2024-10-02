# Target Class Documentation

#### Overview
The `Target` class in the `omath::prediction` namespace represents a target in 3D space with properties such as position, velocity, and whether it is airborne. It provides a method to predict the target's future position based on its current velocity and whether it is affected by gravity (if airborne). This class is used in simulations and games where moving or stationary targets need to be tracked and predicted for projectile aiming systems or physics calculations.

#### Namespace
`omath::prediction`

#### Public Member Variables
1. **`Vector3 m_origin`**: The initial position of the target in 3D space.
2. **`Vector3 m_velocity`**: The velocity of the target, representing how fast and in which direction the target is moving.
3. **`bool m_isAirborne`**: A flag indicating whether the target is airborne (subject to gravity). If `true`, gravity will affect the target’s vertical (z) position over time.

#### Public Methods

1. **`Vector3 PredictPosition(float time, float gravity) const`**:
    - Predicts the future position of the target at a given time, considering its velocity and whether it is affected by gravity.
    - **Parameters**:
        - `time`: The amount of time in the future for which to predict the position.
        - `gravity`: The gravitational constant (e.g., 9.8 m/s²) that applies if the target is airborne.
    - **Returns**: A `Vector3` representing the predicted position of the target at the specified time.

    - **Functionality**:
        - If the target is airborne (`m_isAirborne == true`), its vertical position (`z`) is affected by gravity over time.
        - The target's position is predicted based on its velocity and the time passed. If airborne, gravity is applied to adjust the vertical displacement.

#### Example Usage

```c++
// Initialize a target at position (0, 0, 0) with velocity (10, 0, 5) and airborne
omath::prediction::Target target;
target.m_origin = {0.0f, 0.0f, 0.0f};      // Initial position
target.m_velocity = {10.0f, 0.0f, 5.0f};  // Velocity (10 units/s forward, 5 units/s upward)
target.m_isAirborne = true;               // The target is in the air, affected by gravity

// Predict the position of the target after 2 seconds
float time = 2.0f;
float gravity = 9.8f; // Earth's gravity

omath::Vector3 predictedPosition = target.PredictPosition(time, gravity);
std::cout << "Predicted position: (" << predictedPosition.x << ", " << predictedPosition.y << ", " << predictedPosition.z << ")" << std::endl;
```

#### Key Features
- **Position Prediction**: The `PredictPosition` method allows accurate future position prediction of the target based on velocity and gravity.
- **Airborne Targets**: If the target is airborne, gravity will influence its movement, particularly its vertical (z) displacement, resulting in a more realistic prediction for airborne targets like flying objects or projectiles.

#### Practical Application
The `Target` class is useful in various applications, such as:
- **Projectile Aiming**: Predicting where a moving target will be in the future to calculate an intercept point for a projectile.
- **Physics Simulations**: Modeling the motion of moving objects under gravity, such as falling objects or characters jumping.
- **Game AI**: Used by AI to predict player movement or NPC behavior in games, especially for hit detection and evasion maneuvers.

#### Conclusion:
The `Target` class is an essential part of any system that needs to predict the movement of objects in 3D space, particularly when those objects may be affected by gravity. Its simple interface allows developers to calculate future positions of targets based on their velocity and environmental factors like gravity, making it a useful tool for games, simulations, and physics-based applications.