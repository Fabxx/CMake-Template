add_executable(App src/main.cpp)

cmake_minimum_required(VERSION 3.25)

project(
    WebGPU # name of the project, which will also be the name of the visual studio solution if you use it
    VERSION 0.1.0 # any version number
    LANGUAGES CXX C # programming languages used by the project
)

if (MSVC)
    target_compile_options(App PRIVATE /W4)
else()
    target_compile_options(App PRIVATE -Wall -Wextra -pedantic)
endif()

set_target_properties(App PROPERTIES
    CXX_STANDARD 17
    COMPILE_WARNING_AS_ERROR OFF # sets warnings as errors. Does not allow to compile if warnings are considered errors
)

# add local libraries here. NOTE: Local folder libraries must have a CMakeLists.txt
add_subdirectory(webgpu)
add_subdirectory(glfw3webgpu)

# link libraries

# add extra libraries here
target_link_libraries(App PRIVATE glfw webgpu glfw3webgpu)


# The Application's binary must find wgpu.dll or libwgpu.so at runtime,
# so we automatically copy it (it's called WGPU_RUNTIME_LIB in general)
# next to the binary.
target_copy_webgpu_binaries(App)


