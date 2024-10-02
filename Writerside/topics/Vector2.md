# Vector2 Class Documentation

#### Overview:
The `Vector2` class represents a 2D vector, providing a set of operations for 2D geometry, including vector arithmetic, comparison, and utility functions like normalization and distance calculation. It is designed to handle common vector operations efficiently.

#### Namespace:
`omath`

#### Constructors:
- **`Vector2()`**: Default constructor initializes the vector with `x = 0` and `y = 0`.
- **`Vector2(float x, float y)`**: Constructor to initialize the vector with given `x` and `y` values.

#### Public Member Variables:
- `float x`: The x-coordinate of the vector.
- `float y`: The y-coordinate of the vector.

#### Public Methods:

1. **Equality operators:**
    - `bool operator==(const Vector2& src) const`: Checks if two vectors are equal.
    - `bool operator!=(const Vector2& src) const`: Checks if two vectors are not equal.

2. **Compound assignment operators:**
    - `Vector2& operator+=(const Vector2& v)`: Adds another vector to the current vector.
    - `Vector2& operator-=(const Vector2& v)`: Subtracts another vector from the current vector.
    - `Vector2& operator*=(const Vector2& v)`: Multiplies the current vector by another vector.
    - `Vector2& operator/=(const Vector2& v)`: Divides the current vector by another vector.
    - `Vector2& operator*=(float fl)`: Multiplies the current vector by a scalar.
    - `Vector2& operator/=(float fl)`: Divides the current vector by a scalar.
    - `Vector2& operator+=(float fl)`: Adds a scalar to the vector.
    - `Vector2& operator-=(float fl)`: Subtracts a scalar from the vector.

3. **Basic vector operations:**
    - `float DistTo(const Vector2& vOther) const`: Calculates the Euclidean distance to another vector.
    - `float Length() const`: Returns the length (magnitude) of the vector.
    - `Vector2 Normalized() const`: Returns a normalized version of the vector (with a length of 1).
    - `float Dot(const Vector2& vOther) const`: Calculates the dot product with another vector.
    - `Vector2 Abs()`: Returns the vector with absolute values for each component.
    - `float Sum() const`: Returns the sum of the components (`x + y`).

4. **Arithmetic operators:**
    - `Vector2 operator+(const Vector2& v) const`: Adds two vectors and returns the result.
    - `Vector2 operator-(const Vector2& v) const`: Subtracts two vectors and returns the result.
    - `Vector2 operator*(float fl) const`: Multiplies the vector by a scalar and returns the result.
    - `Vector2 operator/(float fl) const`: Divides the vector by a scalar and returns the result.
    - `Vector2 operator-() const`: Negates the vector (unary minus).

5. **Typecasting:**
    - `template<class type> const type& As() const`: Allows typecasting to other types.
    - `template<class type> type& As()`: Allows typecasting to other types (non-const).

6. **Utility functions:**
    - `std::tuple<float, float> AsTuple() const`: Converts the vector to a tuple.

#### Example Usage:
```c++
omath::Vector2 v1(3.0f, 4.0f);
omath::Vector2 v2(1.0f, 2.0f);

// Adding two vectors
omath::Vector2 v3 = v1 + v2;

// Normalizing a vector
omath::Vector2 normalized = v1.Normalized();

// Calculating the length
float length = v1.Length();
```
