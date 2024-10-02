# Vector4 Class Documentation

#### Overview
The `Vector4` class extends the functionality of `Vector3` to represent a 4D vector by adding the `w` component. It provides various operations for handling 4D vector arithmetic, comparison, and utility functions like normalization and dot product. This class is useful in contexts such as 3D graphics (e.g., handling homogeneous coordinates), physics, and higher-dimensional space calculations.

#### Namespace
`omath`

#### Inheritance
The `Vector4` class inherits from `Vector3`, retaining all functionalities related to 3D vectors while extending it to 4D by adding the `w` component.

#### Constructors
- **`Vector4()`**: Default constructor initializes the vector with `x = 0`, `y = 0`, `z = 0`, and `w = 0`.
- **`Vector4(float x, float y, float z, float w)`**: Constructor to initialize the vector with specific values for `x`, `y`, `z`, and `w`.

#### Public Member Variables
- `float w`: The w-coordinate of the vector.

#### Public Methods

1. **Equality operators:**
    - `bool operator==(const Vector4& src) const`: Checks if two 4D vectors are equal.
    - `bool operator!=(const Vector4& src) const`: Checks if two 4D vectors are not equal.

2. **Compound assignment operators:**
    - `Vector4& operator+=(const Vector4& v)`: Adds another 4D vector to the current vector.
    - `Vector4& operator-=(const Vector4& v)`: Subtracts another 4D vector from the current vector.
    - `Vector4& operator*=(float scalar)`: Multiplies the current vector by a scalar.
    - `Vector4& operator*=(const Vector4& v)`: Multiplies the current vector by another 4D vector.
    - `Vector4& operator/=(float scalar)`: Divides the current vector by a scalar.
    - `Vector4& operator/=(const Vector4& v)`: Divides the current vector by another 4D vector.

3. **Basic vector operations:**
    - `float LengthSqr() const`: Returns the squared length (magnitude) of the vector.
    - `float Length() const`: Returns the length (magnitude) of the vector (implemented in the source file as the square root of `LengthSqr()`).
    - `float Dot(const Vector4& vOther) const`: Computes the dot product between this vector and another 4D vector.
    - `Vector4 Abs()`: Returns the vector with absolute values for each component.
    - `Vector4 Clamp(float min, float max)`: Clamps each component of the vector between `min` and `max`.

4. **Arithmetic operators:**
    - `Vector4 operator+(const Vector4& v) const`: Adds two 4D vectors and returns the result.
    - `Vector4 operator-(const Vector4& v) const`: Subtracts two 4D vectors and returns the result.
    - `Vector4 operator*(float scalar) const`: Multiplies the vector by a scalar and returns the result.
    - `Vector4 operator*(const Vector4& v) const`: Multiplies two 4D vectors component-wise and returns the result.
    - `Vector4 operator/(float scalar) const`: Divides the vector by a scalar and returns the result.
    - `Vector4 operator/(const Vector4& v) const`: Divides two 4D vectors component-wise and returns the result.
    - `Vector4 operator-() const`: Returns the negation of the vector (unary minus).

5. **Utility Functions:**
    - `float Sum() const`: Returns the sum of all components (`x + y + z + w`).

#### Example Usage
```c++
omath::Vector4 v1(1.0f, 2.0f, 3.0f, 4.0f);
omath::Vector4 v2(5.0f, 6.0f, 7.0f, 8.0f);

// Adding two vectors
omath::Vector4 v3 = v1 + v2;

// Calculating the dot product
float dot = v1.Dot(v2);

// Normalizing the vector (if normalization is required, it can be derived from length)
float length = v1.Length();

// Clamping vector values
v1.Clamp(0.0f, 3.0f);
```