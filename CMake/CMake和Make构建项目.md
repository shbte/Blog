### 项目构建命令

~~~bash
1、可以对cmake制定参数，build是Makefile生成路径
    cmake -S . -B build (cmake -Bbuild)
    make -C build
2、执行
    ./bin/cmake_main
~~~

### 根目录文件CMakeLists.txt

~~~makefile
cmake_minimum_required(VERSION 2.8.12)

# 设置cmake项目名(可随意)
project(Cmake_test)

# 设置头文件
# include_directories(include)

# 链接下级文件
add_subdirectory(example)
add_subdirectory(work)

# 如果想使用gdb调试功能，这里必须手动设置成Debug模式
set(CMAKE_BUILD_TYPE Debug)

#设置执行文件输出目录
SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# 设置源文件
AUX_SOURCE_DIRECTORY(. DIR_SRCS)
AUX_SOURCE_DIRECTORY(./example EXAMPLE_DIR_SRCS)
AUX_SOURCE_DIRECTORY(./work WORK_DIR_SRCS)

# 设置编译可执行文件
ADD_EXECUTABLE(cmake_main ${DIR_SRCS} ${EXAMPLE_DIR_SRCS} ${WORK_DIR_SRCS})

# 将库链接进可执行文件中
target_link_libraries(cmake_main example)
target_link_libraries(cmake_main work)
~~~

### 下级目录文件CMakeLists.txt

~~~makefile
# 设置头文件
include_directories(include)

# 添加文件
file(GLOB DIR_MODULE1 "src/*.cpp")

# 添加库
add_library(example ${DIR_MODULE1})
~~~

### 调试器配置文件

~~~json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/bin/cmake_main", //生成的二进制执行文件路径
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}/bin/",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description":  "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ]
        }

    ]
}
~~~
