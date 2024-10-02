# Code Style
### General

This document provides a detailed guide on the coding conventions and style used in the **omath** library. Following a consistent code style is essential for maintaining readability, ensuring maintainability, and facilitating collaboration across multiple developers. This guide covers naming conventions, formatting, comments, and best practices with examples taken from the existing codebase.

---

### 1. **File Structure**

Each header file (`.h`) should include its corresponding implementation file (`.cpp`). For example, the `Vector3.h` file has its implementation in `Vector3.cpp`.

- **Headers**: Used for class declarations, function prototypes, and definitions of inline methods or templates.
- **Source Files**: Used for implementing non-inline methods and detailed logic.

#### Example:
```cpp
// Vector3.h - Header file
namespace omath
{
    class Vector3
    {
    public:
        float x, y, z;
        
        Vector3();
        Vector3(float x, float y, float z);
        Vector3 operator+(const Vector3& other) const;
        float Length() const;
    };
}
```

```cpp
// Vector3.cpp - Source file
#include "Vector3.h"
#include <cmath>

namespace omath
{
    Vector3::Vector3() : x(0), y(0), z(0) {}
    Vector3::Vector3(float x, float y, float z) : x(x), y(y), z(z) {}

    Vector3 Vector3::operator+(const Vector3& other) const
    {
        return {x + other.x, y + other.y, z + other.z};
    }

    float Vector3::Length() const
    {
        return std::sqrt(x * x + y * y + z * z);
    }
}
```

### 2. **Naming Conventions**

#### 2.1 **Classes & Structs**
- Class and struct names use **PascalCase**.
- Class names should be nouns or noun phrases that describe the entity they represent.

**Example**:
```cpp
class Matrix4x4;
struct ViewPort;
```

#### 2.2 **Variables and Member Variables**
- Variable names should use **snake_case**.
- Private member variables should use **m_** as a prefix.

**Example**:
```cpp
float field_of_view;
float m_near_plane_distance;  // private member
```

#### 2.3 **Functions and Methods**
- Function names use **PascalCase** or **camelCase**, depending on their purpose.
    - Public methods should use **PascalCase**.
    - Local functions or utility functions can use **camelCase**.

**Example**:
```cpp
float Length() const;  // public method
float calculatePitchAngle();  // utility function
```

### 3. **Formatting**

#### 3.1 **Indentation**
- Use **4 spaces** for indentation. Do not use tabs.

**Example**:
```cpp
void Matrix::Clear()
{
    for (size_t i = 0; i < 4; ++i)
    {
        for (size_t j = 0; j < 4; ++j)
        {
            data[i][j] = 0.0f;
        }
    }
}
```

#### 3.2 **Braces**
- Opening braces should be placed on the same line as the control statement or function definition.
- Always use braces for control flow statements, even for single-line statements.

**Example**:
```cpp
if (x > 0)
{
    x -= 1;
}
else
{
    x += 1;
}
```

#### 3.3 **Function Definitions**
- For function definitions, the return type should be on the same line as the function name.

**Example**:
```cpp
Vector3 Vector3::operator+(const Vector3& other) const
{
    return {x + other.x, y + other.y, z + other.z};
}
```

#### 3.4 **Line Length**
- Keep lines shorter than **100 characters**. Use line breaks for long expressions or function calls.

**Example**:
```cpp
auto projection_matrix = Matrix::ProjectionMatrix(
    90.0f, 
    viewport.AspectRatio(), 
    0.1f, 
    100.0f
);
```

#### 3.5 **Angle Brackets on New Line**

When using angle brackets for templates, always place them on a **new line** for readability, especially with nested templates.

**Example**:
```cpp
template <typename T>
class Matrix
{
    std::vector
    <
        std::array<T, 4>
    > m_data;
};
```

### 4. **Comments**

#### 4.1 **Inline Comments**
- Inline comments should be used sparingly to explain complex logic or non-obvious code. They should be placed above the code they refer to, rather than on the same line.

**Example**:
```cpp
// Calculate the length of the vector.
float Vector3::Length() const
{
    return std::sqrt(x * x + y * y + z * z);
}
```

#### 4.2 **Function Documentation**
- Each function should have a comment block explaining its purpose, parameters, return value, and any potential side effects. Use a standard format like Doxygen for consistency.

**Example**:
```cpp
/**
 * @brief Calculates the pitch angle required for a projectile to hit a target.
 *
 * @param target_position The position of the target.
 * @param launch_speed The speed at which the projectile is launched.
 * @return The pitch angle in degrees.
 */
float CalculatePitchAngle(const Vector3& target_position, float launch_speed);
```

### 5. **Best Practices**

#### 5.1 **Use of `constexpr` and `const`**
- Use `constexpr` when possible for compile-time evaluations.
- Mark functions and variables `const` wherever applicable.

**Example**:
```cpp
constexpr float PI = 3.14159f;

float Vector3::Length() const
{
    return std::sqrt(x * x + y * y + z * z);
}
```

#### 5.2 **Pass-by-Reference**
- When passing large objects (like vectors or matrices) to functions, prefer passing by `const&` to avoid unnecessary copying.

**Example**:
```cpp
float DotProduct(const Vector3& v1, const Vector3& v2);
```

#### 5.3 **Error Handling**
- Use `std::optional` or `std::expected` for functions that might fail. This ensures that errors are handled explicitly.

**Example**:
```cpp
std::optional<Vector3> CalculateAimPoint(const Projectile& projectile, const Target& target);
```

#### 5.4 **Avoid Magic Numbers**
- Avoid using hardcoded constants. Instead, use named constants or `constexpr` variables.

**Example**:
```cpp
constexpr float gravity = 9.8f;
```

#### 5.5 **Minimize Global Variables**
- Avoid global variables. If shared state is necessary, prefer encapsulating it within a class or struct.

### 6. **Examples from the Codebase**

#### Example 1: Well-Formatted Matrix Class

```cpp
class Matrix
{
public:
    Matrix();
    Matrix(size_t rows, size_t cols);
    
    void Clear();
    float& At(size_t row, size_t col);
    const float& At(size_t row, size_t col) const;

private:
    size_t m_rows;
    size_t m_cols;
    std::vector
    <
        float
    > m_data;
};
```

#### Example 2: Consistent Comment Style

```cpp
/**
 * @brief Transforms a 3D world position into a 2D screen coordinate.
 *
 * @param world_position The position in 3D space.
 * @return std::optional<Vector2> The 2D screen coordinates if the position is visible, std::nullopt otherwise.
 */
std::optional<Vector2> WorldToScreen(const Vector3& world_position) const
{
    // Transformation logic...
    if (isOutsideViewFrustum(world_position))
    {
        return std::nullopt;
    }
    return {transformed_position};
}
```

### Conclusion

By following these coding conventions and best practices, you will ensure that the **omath** codebase remains clean, readable, and maintainable. Consistency in naming, formatting, and comments is critical for a collaborative development environment. As the library grows, adhering to these standards will help keep the project manageable and scalable.