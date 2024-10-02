# Vector3 Class Documentation

#### Overview
The `Vector3` class extends the functionality of `Vector2` to represent a 3D vector, adding operations related to the z-coordinate. It includes various vector operations such as arithmetic, comparison, normalization, and transformations like forward, right, and up vector calculations commonly used in 3D graphics or physics.

#### Namespace
`omath`

#### Inheritance
The `Vector3` class inherits from the `Vector2` class, meaning it retains all operations from `Vector2` and extends them to 3D space by adding the `z` component.

#### Constructors
- **`Vector3()`**: Default constructor initializes the vector with `x = 0`, `y = 0`, and `z = 0`.
- **`Vector3(float x, float y, float z)`**: Initializes the vector with the given `x`, `y`, and `z` values.

#### Public Member Variables
- `float z`: The z-coordinate of the vector.

#### Public Methods

1. **Equality operators:**
    - `bool operator==(const Vector3& src) const`: Checks if two 3D vectors are equal.
    - `bool operator!=(const Vector3& src) const`: Checks if two 3D vectors are not equal.

2. **Compound assignment operators:**
    - `Vector3& operator+=(const Vector3& v)`: Adds another 3D vector to the current vector.
    - `Vector3& operator-=(const Vector3& v)`: Subtracts another 3D vector from the current vector.
    - `Vector3& operator*=(float fl)`: Multiplies the current vector by a scalar.
    - `Vector3& operator*=(const Vector3& v)`: Multiplies the current vector by another 3D vector.
    - `Vector3& operator/=(const Vector3& v)`: Divides the current vector by another 3D vector.
    - `Vector3& operator+=(float fl)`: Adds a scalar to the vector.
    - `Vector3& operator-=(float fl)`: Subtracts a scalar from the vector.
    - `Vector3& operator/=(float fl)`: Divides the vector by a scalar.

3. **Basic vector operations:**
    - `float Length() const`: Returns the length (magnitude) of the vector.
    - `float Length2D() const`: Returns the 2D length (ignoring the z component).
    - `float DistTo(const Vector3& vOther) const`: Computes the distance between this vector and another 3D vector.
    - `float Dot(const Vector3& vOther) const`: Computes the dot product between this vector and another 3D vector.
    - `Vector3 Cross(const Vector3& vOther) const`: Computes the cross product with another 3D vector.
    - `Vector3 Normalized() const`: Returns a normalized version of the vector.

4. **Arithmetic operators:**
    - `Vector3 operator+(const Vector3& v) const`: Adds two 3D vectors and returns the result.
    - `Vector3 operator-(const Vector3& v) const`: Subtracts two 3D vectors and returns the result.
    - `Vector3 operator*(float fl) const`: Multiplies the vector by a scalar and returns the result.
    - `Vector3 operator/(float fl) const`: Divides the vector by a scalar and returns the result.

5. **Angle and Direction Operations:**
    - `Vector3 ViewAngleTo(const Vector3& other) const`: Returns the view angle required to look from the current vector to another vector.
    - `Vector3 ForwardVector(float pitch, float yaw)`: Computes the forward vector from given pitch and yaw angles.
    - `Vector3 RightVector(float pitch, float yaw, float roll)`: Computes the right vector given pitch, yaw, and roll angles.
    - `Vector3 UpVector(float pitch, float yaw, float roll)`: Computes the up vector by combining right and forward vectors.

#### Example Usage
```c++
omath::Vector3 v1(1.0f, 2.0f, 3.0f);
omath::Vector3 v2(4.0f, 5.0f, 6.0f);

// Adding two vectors
omath::Vector3 v3 = v1 + v2;

// Normalizing a vector
omath::Vector3 normalized = v1.Normalized();

// Calculating the dot product
float dot = v1.Dot(v2);

// Calculating the cross product
omath::Vector3 cross = v1.Cross(v2);

// Getting a forward vector based on angles
omath::Vector3 forward = omath::Vector3::ForwardVector(45.0f, 30.0f);
```
