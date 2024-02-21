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

project(HelloWorld)

find_package(fmt CONFIG REQUIRED)

add_executable(HelloWorld main.cpp)

target_link_libraries(HelloWorld PRIVATE fmt::fmt)
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
