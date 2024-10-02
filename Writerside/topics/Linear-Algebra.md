# Linear Algebra

#### Overview
Linear algebra is a branch of mathematics focused on vectors, matrices, and operations on these structures. It forms the foundation of many critical operations in computer graphics, physics simulations, game development, and other computational applications. Vectors and matrices are essential tools for representing and transforming geometric data, such as points, directions, and transformations in 2D and 3D spaces.

In this topic, we will cover key concepts related to vectors and matrices, their operations, and how they are implemented through classes such as `Vector2`, `Vector3`, `Vector4`, `Matrix`, and `Mat`.

#### Vectors
A **vector** is a quantity defined by its magnitude and direction, typically represented as an ordered set of components (e.g., x, y, z for 3D vectors). Vectors are used to represent points in space, velocities, forces, and directions.

##### Vector2 Class
The `Vector2` class represents a 2D vector with `x` and `y` components. It supports vector arithmetic, such as addition, subtraction, scalar multiplication, and dot products, along with utility functions like normalization and distance calculation.

##### Vector3 Class
The `Vector3` class extends the 2D vector into 3D by adding a `z` component. This class is widely used in 3D graphics to represent positions, directions (e.g., forward, up, right), and rotations.

##### Vector4 Class
The `Vector4` class represents a 4D vector, extending the concept of 3D vectors by introducing a `w` component. This class is commonly used in homogeneous coordinates, which simplify matrix transformations in 3D graphics. Homogeneous coordinates are crucial for operations like translation, rotation, and perspective projection.

#### Matrices
A **matrix** is a rectangular array of numbers arranged in rows and columns. Matrices are used to perform transformations (translation, scaling, rotation) on vectors and points in space. In computer graphics, matrices enable the manipulation of objects within a scene, camera views, and projections onto 2D screens.

##### Matrix Class
The `Matrix` class provides a dynamic matrix structure capable of representing matrices of arbitrary size. It includes operations such as matrix multiplication, transposition, and determinant calculation. This class is particularly useful for general linear algebra tasks in graphics pipelines.

##### Mat Class
The `Mat` class is a templated fixed-size matrix class, allowing for compile-time dimensions and operations. It is designed to provide an efficient and flexible solution for common matrix operations in 3D graphics.

#### Linear Algebra in 3D Graphics
In 3D graphics, linear algebra is fundamental to transforming objects in a scene. These transformations include scaling, rotating, and translating objects, all of which are achieved using matrices. The matrices can then be multiplied with vectors to apply the transformations to points in space.

1. **Translation**: Moving an object in space is done by multiplying the object’s points by a translation matrix.
2. **Rotation**: Rotating an object is done through rotation matrices, which are derived from trigonometric functions.
3. **Scaling**: Changing the size of an object involves scaling matrices that stretch or shrink points proportionally.
4. **Projection**: Projecting a 3D scene onto a 2D screen uses a perspective projection matrix, which simulates the effect of distance (objects further away appear smaller).

These operations are vital in modern graphics engines, where complex scenes require transformations for every object, camera, and lighting element.

#### Example of a Graphics Pipeline
1. **Modeling**: 3D objects are defined in model space using vectors and matrices.
2. **World Transformation**: Objects are transformed from model space to world space via translation, rotation, and scaling matrices.
3. **Camera Transformation**: Objects are further transformed from world space to camera space, where the camera is treated as the origin.
4. **Projection**: The scene is projected onto a 2D screen using a projection matrix.
5. **Rasterization**: Finally, the 2D representation is converted to pixels for display.

#### Conclusion
Linear algebra forms the backbone of many operations in computer graphics and simulations. By understanding and utilizing vectors and matrices, developers can efficiently model, transform, and render complex 3D scenes. The `Vector2`, `Vector3`, `Vector4`, `Matrix`, and `Mat` classes are key tools that make these computations easier and more efficient, enabling the development of visually rich and physically accurate simulations and games.

Understanding the operations on these mathematical constructs will unlock new possibilities in graphics programming and provide the foundation for working with more advanced techniques like ray tracing, physics simulations, and machine learning.