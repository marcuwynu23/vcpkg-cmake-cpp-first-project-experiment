# How to create c/c++ project using vcpkg

1. create a project folder

```sh
mkdir project
```

2. navigate to project folder

```sh
cd project
```

3. initialize vcpkg project

```sh
vcpkg new --application
```

4. add ports (dependencies. ex. fmt,libssh,boost)

```sh
vckg add port fmt
```

5. create cmakelists.txt

```cmake
cmake_minimum_required(VERSION 3.10)

# set the project name
project(app)

# add the executable
# Include source files from the 'app' directory
file(GLOB APP_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
add_executable(app ${APP_SOURCES})

# add header files
target_include_directories(app PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

# find and link fmt library
find_package(fmt CONFIG REQUIRED)
target_link_libraries(app PRIVATE fmt::fmt)

```

6. create CMakePresets.json

```json
{
  "version": 3,
  "configurePresets": [
    {
      "name": "default",
      "binaryDir": "${sourceDir}/build",
      "cacheVariables": {
        "CMAKE_TOOLCHAIN_FILE": "$env{VCPKG_ROOT}/scripts/buildsystems/vcpkg.cmake"
      }
    }
  ]
}
```

7. create c/c++ entry point (main.cpp/main.c)

```sh
touch main.cpp
```

8. write code in main.cpp

```cpp
#include <fmt/core.h>

int main()
{
	fmt::print("Hello World!\n");
	return 0;
}
```

9. generate build files using cmake based on **CMakePresets.json** configuration.

```sh
cmake --preset=default
```

10. build the project

```sh
cmake --build build
```

11. run the app

```sh
./build/debug/hello.exe
```
