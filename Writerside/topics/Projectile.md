# Projectile Class Documentation

#### Overview
The `Projectile` class in the `omath::prediction` namespace represents a projectile with certain properties such as origin, launch speed, and gravity scale. It provides functionality to predict the position of the projectile over time based on initial launch conditions (pitch, yaw, and gravity). This class is typically used in simulations where projectile motion, influenced by gravity, needs to be calculated, such as in games, physics engines, and ballistic trajectory simulations.

#### Namespace
`omath::prediction`

#### Public Member Variables
1. **`Vector3 m_origin`**: The initial position (origin) of the projectile in 3D space.
2. **`float m_launchSpeed`**: The initial speed of the projectile when it is launched.
3. **`float m_gravityScale`**: A scaling factor for the gravitational force acting on the projectile. This allows for adjusting gravity strength, which can be useful in different simulation scenarios (e.g., when simulating projectiles on planets with different gravities or altering gravity in games).

#### Public Methods

1. **`Vector3 PredictPosition(float pitch, float yaw, float time, float gravity) const`**:
    - Predicts the position of the projectile at a given time, based on the initial launch conditions (pitch, yaw, and gravity).
    - **Parameters**:
        - `pitch`: The launch angle in the vertical plane, in degrees.
        - `yaw`: The launch angle in the horizontal plane, in degrees.
        - `time`: The elapsed time since the projectile was launched.
        - `gravity`: The gravitational acceleration constant (e.g., 9.8 m/s²).
    - **Returns**: A `Vector3` representing the predicted position of the projectile at the specified time.

#### Example Usage
To use the `Projectile` class, initialize a projectile with an origin, launch speed, and gravity scale. Then use the `PredictPosition` method to calculate its position over time.

```c++
// Create a projectile at origin with a launch speed of 30 m/s and normal gravity scale
omath::prediction::Projectile projectile;
projectile.m_origin = {0.0f, 0.0f, 0.0f};
projectile.m_launchSpeed = 30.0f;
projectile.m_gravityScale = 1.0f;  // Normal Earth gravity

// Predict the position of the projectile after 2 seconds with pitch 45 degrees and yaw 0 degrees
float pitch = 45.0f;
float yaw = 0.0f;
float time = 2.0f;
float gravity = 9.8f;

omath::Vector3 predictedPosition = projectile.PredictPosition(pitch, yaw, time, gravity);
std::cout << "Predicted position: (" << predictedPosition.x << ", " << predictedPosition.y << ", " << predictedPosition.z << ")" << std::endl;
```

#### Key Features
- **Position Prediction**: The `PredictPosition` method allows for real-time simulation of the projectile's trajectory based on launch conditions and the influence of gravity.
- **Gravity Scaling**: The `m_gravityScale` member variable allows for adjusting how much gravity affects the projectile, making the class flexible for use in different simulation environments.

#### Practical Application
The `Projectile` class is ideal for use in games and simulations where predicting the motion of objects under the influence of gravity is important. Examples include:
- **Ballistics**: Predicting the trajectory of a bullet, arrow, or any other projectile.
- **Game Physics**: Simulating the motion of objects affected by gravity, like grenades or thrown items.
- **Simulation Software**: Calculating trajectories in educational or scientific applications.

#### Conclusion
The `Projectile` class provides a simple yet powerful way to simulate and predict the behavior of projectiles in 3D space. It takes into account initial launch conditions, gravity, and time, making it suitable for various applications in game development, physics simulations, and more. By using the `PredictPosition` method, developers can accurately model the behavior of projectiles and account for real-world physics like gravity.