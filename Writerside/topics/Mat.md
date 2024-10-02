# Mat Class Documentation

#### Overview
The `Mat` class is a templated matrix class that allows creating fixed-size matrices of arbitrary dimensions, providing a wide range of matrix operations for use in mathematical computations. It supports operations like matrix initialization, element access, matrix multiplication, and the creation of common matrices such as screen, translation, orientation, and projection matrices. The class is fully constexpr where possible, making it efficient for compile-time matrix computations.

#### Namespace
`omath`

#### Template Parameters
- **`Rows`**: The number of rows in the matrix.
- **`Columns`**: The number of columns in the matrix.

#### Constructors
1. **`Mat()`**: Default constructor that initializes all elements to zero.
2. **`Mat(const std::initializer_list<std::initializer_list<float>>& rows)`**: Initializes the matrix from a nested initializer list, ensuring that the dimensions match the template parameters.
3. **`Mat(const Mat& other)`**: Copy constructor that creates a new matrix as a copy of another matrix.
4. **`Mat(Mat&& other) noexcept`**: Move constructor for efficient resource transfer.

#### Static Methods
1. **`static Mat<4, 4> ToScreenMat(float screenWidth, float screenHeight)`**: Generates a 4x4 matrix that transforms points into screen coordinates based on the screen width and height.

2. **`static Mat<4, 4> TranslationMat(const Vector3& diff)`**: Creates a 4x4 translation matrix using the given `Vector3` displacement.

3. **`static Mat<4, 4> OrientationMat(const Vector3& forward, const Vector3& right, const Vector3& up)`**: Generates an orientation matrix using the provided forward, right, and up vectors, useful in 3D graphics transformations.

4. **`static Mat<4, 4> ProjectionMat(float fieldOfView, float aspectRatio, float near, float far)`**: Creates a perspective projection matrix using field of view, aspect ratio, and near/far clipping planes.

#### Public Methods

1. **Matrix Size and Element Access:**
    - **`constexpr size_t RowCount() noexcept`**: Returns the number of rows in the matrix.
    - **`constexpr size_t ColumnsCount() noexcept`**: Returns the number of columns in the matrix.
    - **`constexpr std::pair<size_t, size_t> Size() noexcept`**: Returns a pair representing the matrix's dimensions.
    - **`constexpr float& At(size_t rowIndex, size_t columnIndex)`**: Provides access to an element at the specified row and column index. Throws an exception if the indices are out of bounds.
    - **`constexpr const float& At(size_t rowIndex, size_t columnIndex) const`**: Provides read-only access to an element at the specified row and column index.

2. **Matrix Operations:**
    - **`Mat operator+(const Mat& other) const`**: Adds two matrices element-wise and returns the result.
    - **`Mat operator-(const Mat& other) const`**: Subtracts two matrices element-wise and returns the result.
    - **`Mat operator*(const Mat& other) const`**: Multiplies two matrices together and returns the result. Ensures compatibility between the dimensions of the matrices.
    - **`Mat& operator*=(const Mat& other)`**: Multiplies two matrices and assigns the result to the current matrix.
    - **`Mat operator*(float scalar) const`**: Multiplies all elements of the matrix by a scalar and returns the result.
    - **`Mat& operator*=(float scalar)`**: Multiplies all elements by a scalar and assigns the result to the current matrix.

3. **Utility Functions:**
    - **`void Clear()`**: Sets all elements in the matrix to zero.
    - **`std::string ToString() const`**: Returns a string representation of the matrix for debugging or logging purposes.

#### Private Members
- **`std::array<float, Rows * Columns> m_data`**: Stores the elements of the matrix in a contiguous block of memory for efficient access and manipulation.

#### Example Usage

```c++
// Creating a 4x4 translation matrix
omath::Mat<4, 4> translation = omath::Mat<4, 4>::TranslationMat({1.0f, 2.0f, 3.0f});

// Creating a projection matrix
omath::Mat<4, 4> projection = omath::Mat<4, 4>::ProjectionMat(45.0f, 1.6f, 0.1f, 100.0f);

// Accessing elements of the matrix
float element = translation.At(0, 3);  // Accessing the translation component

// Matrix multiplication
omath::Mat<4, 4> result = translation * projection;

// Displaying the matrix
std::string matrixStr = result.ToString();
std::cout << matrixStr << std::endl;
```

This `Mat` class provides a flexible and efficient structure for working with matrices in various applications, especially in 3D graphics and transformations. The template design allows for matrices of arbitrary dimensions, while the static methods help generate common transformation matrices.