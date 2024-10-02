# Camera Class Documentation

#### Overview
The `Camera` class in the `omath::projection` namespace is responsible for simulating a camera in 3D space. It allows for viewing the scene from different perspectives, defined by the camera's position, view angles, and projection parameters such as field of view and clipping planes. The camera generates the view matrix used for transforming 3D world coordinates into the camera's perspective, and it provides functionality to convert world coordinates to screen space for rendering.

#### Namespace
`omath::projection`

#### Constructors

1. **`Camera(const Vector3& position, const Vector3& viewAngles, const ViewPort& viewPort, float fov, float near, float far)`**:
    - **`position`**: The initial position of the camera in 3D space.
    - **`viewAngles`**: The viewing angles of the camera, represented as a `Vector3` (pitch, yaw, roll).
    - **`viewPort`**: A `ViewPort` object representing the screen's width, height, and aspect ratio.
    - **`fov`**: The field of view (FOV) in degrees, which controls how wide the camera's view is.
    - **`near`**: The near clipping plane, representing the closest distance at which objects are visible.
    - **`far`**: The far clipping plane, representing the farthest distance at which objects are still rendered.

#### Public Methods

1. **`void SetViewAngles(const Vector3& viewAngles)`**:
    - Sets the camera's view angles. This defines the camera's orientation in space, with pitch controlling the vertical angle, yaw controlling the horizontal angle, and roll controlling the rotation around the camera's forward axis.

2. **`[[nodiscard]] Mat<4, 4> GetViewMatrix() const`**:
    - Generates and returns the view matrix. The view matrix is used to transform world coordinates into the camera's coordinate space, allowing objects in the scene to be rendered from the camera's perspective.

3. **`[[nodiscard]] std::expected<Vector2, Error> WorldToScreen(const Vector3& worldPosition) const`**:
    - Converts a 3D world position into 2D screen coordinates. This method projects a point in 3D space onto the camera's screen, returning the 2D position on the screen where the world point would be rendered.
    - **Returns**: A `Vector2` representing the screen position if the conversion is successful, or an `Error` code if the point cannot be projected (e.g., it's outside the camera's view or behind the camera).

#### ViewPort Class

The `ViewPort` class defines the screen's dimensions and provides the **aspect ratio**, which is essential for rendering and projection calculations.

- **`float m_width`**: The width of the viewport (screen).
- **`float m_height`**: The height of the viewport.
- **`AspectRatio()`**: Returns the aspect ratio of the viewport, calculated as width divided by height.

#### Member Variables

- **`ViewPort m_viewPort`**: The viewport associated with the camera, defining the screen's size and aspect ratio.
- **`float m_fieldOfView`**: The field of view (FOV) of the camera in degrees.
- **`float m_nearPlaneDistance`**: The distance to the near clipping plane.
- **`float m_farPlaneDistance`**: The distance to the far clipping plane.
- **`Vector3 m_viewAngles`**: The current viewing angles of the camera, representing its orientation in 3D space.
- **`Vector3 m_origin`**: The current position of the camera in the 3D world.

#### Example Usage

```c++
// Define the camera position, view angles, and viewport
omath::Vector3 cameraPosition = {0.0f, 0.0f, 5.0f};
omath::Vector3 viewAngles = {0.0f, 0.0f, 0.0f};  // No rotation
omath::projection::ViewPort viewPort = {800.0f, 600.0f};  // 800x600 viewport

// Create a camera with a 90-degree FOV, near plane at 0.1 and far plane at 100
omath::projection::Camera camera(cameraPosition, viewAngles, viewPort, 90.0f, 0.1f, 100.0f);

// Set new view angles (e.g., look slightly upward)
camera.SetViewAngles({10.0f, 0.0f, 0.0f});

// Get the view matrix for transforming world coordinates
omath::Mat<4, 4> viewMatrix = camera.GetViewMatrix();

// Convert a world position to screen coordinates
omath::Vector3 worldPosition = {0.0f, 0.0f, 10.0f};  // A point in the scene
auto screenPosition = camera.WorldToScreen(worldPosition);

if (screenPosition) {
    std::cout << "Screen position: (" << screenPosition->x << ", " << screenPosition->y << ")" << std::endl;
} else {
    std::cout << "Point is outside the camera's view" << std::endl;
}
```

#### Key Features

- **View Matrix**: The camera provides the view matrix, which transforms world space coordinates into camera space. This is essential for rendering scenes from the camera’s perspective.
- **World to Screen Conversion**: The `WorldToScreen` method projects 3D points onto the 2D screen, allowing for precise mapping of objects from world coordinates to screen coordinates.
- **Clipping Planes**: The near and far clipping planes define the range of distances at which objects are rendered, providing control over what parts of the scene are visible.

#### Practical Application

The `Camera` class is an essential component in 3D rendering systems, allowing the simulation of a virtual camera that views and captures the scene. It is used in:
- **3D Game Development**: Simulating a player's or NPC's viewpoint.
- **Simulation Systems**: Creating realistic views in simulations of real-world environments.
- **Rendering Pipelines**: Transforming 3D scenes into 2D images for display on a screen.

#### Conclusion

The `Camera` class in the `omath::projection` module provides a comprehensive and flexible way to simulate a virtual camera in 3D space. By defining a position, viewing angles, field of view, and clipping planes, this class allows developers to transform world coordinates into camera space and project them onto a 2D screen, making it an indispensable tool for 3D rendering, simulations, and games.