# Engine Documentation

#### Overview
The `Engine` class in the `omath::prediction` namespace is responsible for calculating the optimal trajectory and aiming point for a projectile to hit a moving or stationary target. It simulates the motion of the projectile under the influence of gravity, considering factors such as launch speed, gravity, and tolerance levels. This class is typically used in applications like physics simulations, games, or ballistic predictions where accurate projectile behavior is needed.

#### Namespace
`omath::prediction`

#### Constructors
1. **`Engine(float gravityConstant, float simulationTimeStep, float maximumSimulationTime, float distanceTolerance)`**:
    - **`gravityConstant`**: The gravitational acceleration constant (e.g., 9.8 m/s²).
    - **`simulationTimeStep`**: The time step for each simulation iteration (used for calculating the projectile's path).
    - **`maximumSimulationTime`**: The maximum time allowed for simulating the projectile's flight before terminating the prediction.
    - **`distanceTolerance`**: The tolerance level for determining if the projectile has reached the target.

#### Public Methods

1. **`std::optional<Vector3> MaybeCalculateAimPoint(const Projectile& projectile, const Target& target) const`**:
    - Calculates the best aiming point to hit the target given the projectile's properties and the target's position/motion.
    - Returns an optional `Vector3` containing the calculated aim point in 3D space.
    - If the prediction fails (e.g., if the target is unreachable due to range or constraints), it returns `std::nullopt`.

#### Private Methods

1. **`std::optional<float> MaybeCalculateProjectileLaunchPitchAngle(const Projectile& projectile, const Vector3& targetPosition) const`**:
    - Calculates the launch angle (pitch) required for the projectile to hit the target at the given position.
    - Returns an optional `float` representing the pitch angle in degrees. If no valid angle is found (e.g., due to range or gravity constraints), it returns `std::nullopt`.

2. **`bool IsProjectileReachedTarget(const Vector3& targetPosition, const Projectile& projectile, float pitch, float time) const`**:
    - Determines whether the projectile reaches the target at a given time, considering the launch pitch and projectile characteristics.
    - Returns `true` if the projectile reaches the target within the given distance tolerance, and `false` otherwise.

#### Example Workflow
To predict the trajectory and aim for a projectile, the engine uses the following steps:
1. **Input the projectile's properties**: The engine is provided with the projectile's initial speed, launch conditions, and the target's position and velocity (if moving).
2. **Calculate the pitch angle**: The engine attempts to compute a suitable pitch angle that will guide the projectile to the target. This takes into account gravity and the projectile's properties.
3. **Simulate the trajectory**: With the calculated angle, the engine simulates the projectile's flight, step by step, using the time step defined during initialization.
4. **Check if the projectile hits the target**: The simulation checks whether the projectile reaches the target within the specified distance tolerance.
5. **Return the aim point**: If the target is reachable, the engine provides the aim point for launching the projectile; otherwise, no solution is returned.

#### Example Usage
```c++
omath::prediction::Projectile projectile(30.0f);  // Projectile with an initial speed of 30 m/s
omath::prediction::Target target({50.0f, 0.0f, 20.0f});  // Stationary target at a specific position

// Create the prediction engine with gravity, timestep, max time, and tolerance
omath::prediction::Engine engine(9.8f, 0.1f, 10.0f, 0.5f);

// Try to calculate the aim point to hit the target
auto aimPoint = engine.MaybeCalculateAimPoint(projectile, target);

if (aimPoint) {
    std::cout << "Aim at position: " << aimPoint->x << ", " << aimPoint->y << ", " << aimPoint->z << std::endl;
} else {
    std::cout << "Target unreachable" << std::endl;
}
```

#### Key Components
- **Gravity Constant**: The engine simulates projectile motion under gravity, which significantly affects the trajectory.
- **Time Step and Maximum Simulation Time**: These parameters define how the simulation is run step-by-step and how long the simulation should attempt to reach the target.
- **Distance Tolerance**: The engine considers the projectile as having reached the target if it is within a certain distance, defined by the `distanceTolerance` parameter. This is useful for real-world scenarios where perfect precision is not required.

#### Conclusion
The `Engine` class provides a robust solution for predicting projectile trajectories and calculating the optimal aim point for a given target. It takes into account key physical factors such as gravity, time, and distance tolerance, making it useful in games, simulations, and physics-based applications where accurate projectile prediction is needed.