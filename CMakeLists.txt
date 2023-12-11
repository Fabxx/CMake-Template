add_executable(App src/main.cpp)

cmake_minimum_required(VERSION 3.25)

project(
    namehere # name of the project, which will also be the name of the visual studio solution if you use it
    VERSION 0.1.0 # any version number
    LANGUAGES CXX C # programming languages used by the project
)
# Compiler usage
if (MSVC)
    target_compile_options(App PRIVATE /W4)
else()
    target_compile_options(App PRIVATE -Wall -Wextra -pedantic)
endif()

# Language standard definition and warning flags
set_target_properties(App PROPERTIES
    CXX_STANDARD 17
    COMPILE_WARNING_AS_ERROR OFF # sets warnings as errors. Does not allow to compile if warnings are considered errors
)

# add local libraries here. NOTE: Local folder libraries must have a CMakeLists.txt
add_subdirectory(dirname)

# add extra libraries here
target_link_libraries(App PRIVATE name1 name2 name3)
