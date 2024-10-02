# Matrix Class Documentation

#### Overview:
The `Matrix` class provides a flexible and powerful way to represent and manipulate 2D matrices, primarily designed for mathematical and graphical computations. The class supports various operations like matrix multiplication, transposition, determinants, and specialized matrices such as translation and projection matrices, which are essential in 3D graphics and linear algebra.

#### Namespace:
`omath`

#### Constructors:
1. **`Matrix()`**: Default constructor that creates an empty matrix with no rows or columns.
2. **`Matrix(size_t rows, size_t columns)`**: Constructor that initializes a matrix with a specified number of rows and columns, filled with zeros.
3. **`Matrix(const std::initializer_list<std::initializer_list<float>>& rows)`**: Constructor that initializes the matrix with a list of rows.
4. **`Matrix(const Matrix& other)`**: Copy constructor to create a matrix from another matrix.
5. **`Matrix(Matrix&& other) noexcept`**: Move constructor for efficient transfer of matrix resources.
6. **`Matrix(size_t rows, size_t columns, const float* pRaw)`**: Initializes the matrix with data from a raw pointer array.

#### Public Static Methods:
1. **`static Matrix ToScreenMatrix(float screenWidth, float screenHeight)`**: Generates a matrix that transforms points into screen coordinates based on the screen width and height.

2. **`static Matrix TranslationMatrix(const Vector3& diff)`**: Creates a translation matrix that translates points by a given `Vector3` displacement.

3. **`static Matrix OrientationMatrix(const Vector3& forward, const Vector3& right, const Vector3& up)`**: Creates an orientation matrix using the provided forward, right, and up vectors, often used in 3D graphics.

4. **`static Matrix ProjectionMatrix(float fieldOfView, float aspectRatio, float near, float far)`**: Generates a perspective projection matrix using field of view, aspect ratio, and near/far clipping planes.

#### Public Methods:

1. **Matrix Dimension and Access:**
    - **`size_t RowCount() const noexcept`**: Returns the number of rows in the matrix.
    - **`size_t ColumnsCount() const noexcept`**: Returns the number of columns in the matrix.
    - **`std::pair<size_t, size_t> Size() const noexcept`**: Returns a pair representing the matrix's dimensions.
    - **`float& At(size_t iRow, size_t iCol)`**: Returns a reference to the element at the specified row and column.
    - **`const float& At(size_t iRow, size_t iCol) const`**: Returns a const reference to the element at the specified row and column.

2. **Matrix Operations:**
    - **`Matrix Transpose() const`**: Returns the transpose of the matrix (swapping rows and columns).
    - **`Matrix operator*(const Matrix& other) const`**: Matrix multiplication operator that multiplies two matrices.
    - **`Matrix& operator*=(const Matrix& other)`**: Matrix multiplication and assignment.
    - **`Matrix operator*(float f) const`**: Multiplies all elements of the matrix by a scalar.
    - **`Matrix& operator*=(float f)`**: Scalar multiplication and assignment.
    - **`Matrix& operator/=(float f)`**: Scalar division and assignment.

3. **Matrix Data Management:**
    - **`void SetDataFromRaw(const float* pRawMatrix)`**: Populates the matrix using data from a raw pointer array.
    - **`void Set(float val)`**: Sets all elements in the matrix to a specific value.
    - **`void Clear()`**: Clears the matrix, resetting it to an empty state.
    - **`const float* Raw() const`**: Returns a raw pointer to the matrix data.

4. **Matrix Minor and Determinants:**
    - **`Matrix Strip(size_t row, size_t column) const`**: Returns a matrix that is the original matrix with the specified row and column removed (used in determinant calculations).
    - **`float Minor(size_t i, size_t j) const`**: Computes the minor of the matrix at the given row and column.
    - **`float AlgComplement(size_t i, size_t j) const`**: Computes the algebraic complement for the matrix at the given row and column.
    - **`float Determinant() const`**: Computes the determinant of the matrix.

5. **Other Utilities:**
    - **`float Sum() const`**: Returns the sum of all elements in the matrix.

#### Example Usage:

```c++
omath::Matrix m1(4, 4);  // Create a 4x4 matrix
omath::Matrix m2 = omath::Matrix::TranslationMatrix({1.0f, 2.0f, 3.0f});  // Translation matrix

// Matrix multiplication
omath::Matrix result = m1 * m2;

// Getting an element and modifying it
float value = m1.At(0, 1);
m1.At(0, 1) = 5.0f;

// Transposing a matrix
omath::Matrix transpose = m1.Transpose();

// Computing a determinant
float det = m2.Determinant();
```

#### Special Matrix Types:
- **Screen Matrix**: Used for transforming points to screen coordinates.
- **Translation Matrix**: Translates points in 3D space.
- **Orientation Matrix**: Adjusts the orientation of a 3D object in space.
- **Projection Matrix**: Used for 3D perspective projections.
