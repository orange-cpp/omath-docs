# Getting Started
### Getting Started with Orange's Math Library (omath)

This guide will walk you through the process of cloning, configuring, building, and installing the **omath** library using CMake presets. The library supports both Windows and Linux platforms, and you can use either **Debug** or **Release** configurations. We'll cover the steps in detail and explain how to customize the build process with additional CMake options.

---

#### Prerequisites

Before you begin, make sure you have the following tools installed:

- **C++ Compiler**: A modern C++ compiler (e.g., GCC, Clang, or MSVC) with support for C++17 or newer.
- **CMake**: A build system generator. Ensure that **CMake 3.15** or later is installed.
- **Ninja** (optional but recommended): A fast build system that is often used in combination with CMake.

---

### Step 1: Clone the Repository

To get started, clone the omath repository from GitHub:

```bash
git clone https://github.com/orange-cpp/omath.git
cd omath
```

This will download the source code into the `omath` directory.

---

### Step 2: Configure the Build Using CMake Presets

The **omath** library uses **CMake Presets** to simplify the build process. Several presets are available for both Windows and Linux, providing configurations for **Debug** and **Release** builds.

#### Available Build Presets

- **Windows**:
    - `windows-debug`: Debug build for development and debugging.
    - `windows-release`: Release build optimized for performance.

- **Linux**:
    - `linux-debug`: Debug build for development and debugging.
    - `linux-release`: Release build optimized for performance.

You can list all available presets with the following command:

```bash
cmake --list-presets
```

---

### Step 3: Configure the Build

Use one of the following commands to configure the project based on your platform and desired build type.

#### For **Windows**:

- **Debug Build**:
  ```bash
  cmake --preset windows-debug
  ```

- **Release Build**:
  ```bash
  cmake --preset windows-release
  ```

#### For **Linux**:

- **Debug Build**:
  ```bash
  cmake --preset linux-debug
  ```

- **Release Build**:
  ```bash
  cmake --preset linux-release
  ```

This command configures the project using the preset of your choice. It automatically generates the build files and stores them in the corresponding binary directory (e.g., `cmake-build/build/windows-debug`).

---

### Step 4: Build the Project

After configuring the project, you can build it using the following command:

```bash
cmake --build cmake-build/build/<preset> --target all -j <number_of_cores>
```

Replace `<preset>` with the specific preset you used (e.g., `windows-release` or `linux-debug`) and `<number_of_cores>` with the number of parallel jobs you want to run (adjust this based on your CPU’s number of cores).

#### Example for **Windows Release** Build:

```bash
cmake --build cmake-build/build/windows-release --target all -j 6
```

#### Example for **Linux Debug** Build:

```bash
cmake --build cmake-build/build/linux-debug --target all -j 4
```

The `-j` flag controls the number of parallel jobs during compilation, speeding up the build process. Adjust this number based on the available CPU cores on your system.

---

### Step 5: Install the Build (Optional)

If you want to install the library to a specific directory, you can use the following command:

```bash
cmake --install cmake-build/build/<preset>
```

This command will install the built artifacts (binaries, libraries, and headers) to the directory specified in the preset. You can also customize the install directory by using the `CMAKE_INSTALL_PREFIX` option.

#### Example:

```bash
cmake --install cmake-build/build/linux-release
```

---

### Customizing the Build

You can further customize the build process by passing additional CMake options during configuration. Below are some commonly used options:

#### 1. **CMAKE_BUILD_TYPE**:
Override the build type if you're not using a preset.

```bash
cmake -DCMAKE_BUILD_TYPE=Release -S . -B build/release
```

#### 2. **CMAKE_INSTALL_PREFIX**:
Set a custom installation directory.

```bash
cmake -DCMAKE_INSTALL_PREFIX=/path/to/install -S . -B build/install
```

#### 3. **BUILD_SHARED_LIBS**:
Build shared libraries instead of static libraries.

```bash
cmake -DBUILD_SHARED_LIBS=ON -S . -B build/shared
```

#### 4. **CMAKE_EXPORT_COMPILE_COMMANDS**:
Generate a `compile_commands.json` file for tools like clang-tidy or IDEs that support code analysis.

```bash
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON -S . -B build/analysis
```

#### 5. **Using Ninja**:
By default, the presets are set up to use **Ninja** as the build system. If you prefer to use another build system, such as **Makefiles**, you can specify the generator manually.

```bash
cmake -G "Unix Makefiles" --preset linux-debug
```

---

### Step 6: Running Tests (Optional)

After building the project, you can run unit tests to ensure the library is functioning correctly:

```bash
cmake --build cmake-build/build/<preset> --target test
```

This will execute all tests defined in the project.

---

### Conclusion

By following this guide, you should be able to clone, configure, build, and install the **omath** library on both Windows and Linux. The use of CMake presets simplifies the process, allowing for quick configuration of Debug or Release builds. You can also customize the build process using additional CMake options to suit your development needs.