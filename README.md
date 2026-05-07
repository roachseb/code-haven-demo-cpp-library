# math-utils

A simple C++ math utilities library — Code Haven demo project.

## Using this library in your project

### Option 1: CMake FetchContent (recommended)

```cmake
include(FetchContent)
FetchContent_Declare(math-utils
    GIT_REPOSITORY https://github.com/roachseb/code-haven-demo-cpp-library.git
    GIT_TAG v1.0.0  # pin to a release tag
)
FetchContent_MakeAvailable(math-utils)

target_link_libraries(your_app PRIVATE math-utils)
```

### Option 2: Pre-built release tarball

Download from the [Releases page](../../releases):

```bash
wget https://github.com/roachseb/code-haven-demo-cpp-library/releases/download/v1.0.0/code-haven-demo-cpp-library-1.0.0-linux-x64.tar.gz
tar xzf code-haven-demo-cpp-library-*.tar.gz -C /usr/local
```

Then in your CMakeLists.txt:
```cmake
find_package(math-utils REQUIRED)
target_link_libraries(your_app PRIVATE math-utils::math-utils)
```

### Option 3: Conan (if configured)

```
[requires]
math-utils/1.0.0

[generators]
CMakeDeps
CMakeToolchain
```

## API

```cpp
#include "math_utils/math_utils.h"

math_utils::add(2, 3);        // → 5
math_utils::subtract(5, 3);   // → 2
math_utils::multiply(3, 4);   // → 12
math_utils::divide(10, 2);    // → 5
math_utils::factorial(5);     // → 120
math_utils::is_prime(17);     // → true
math_utils::gcd(12, 8);       // → 4
```

## Building locally

```bash
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build
ctest --test-dir build --output-on-failure
```

## Formatting

```bash
clang-format -i src/*.cpp include/**/*.h tests/*.cpp
```
