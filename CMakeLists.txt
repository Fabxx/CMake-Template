cmake_minimum_required(VERSION 3.25)

project(
    App # name of the project, which will also be the name of the visual studio solution if you use it
    VERSION 0.1.0 # any version number
    LANGUAGES CXX C # programming languages used by the project
)

# MUST be set before target compile options to define executable name.
add_executable(App src/main.cpp)

# Compiler usage
if (MSVC)
    target_compile_options(App PRIVATE /W4)
else()
    target_compile_options(App PRIVATE -Wall -Wextra -pedantic)
endif()

# Language standard definition and warning flags
# sets warnings as errors. Does not allow to compile if warnings are considered errors
set_target_properties(App PROPERTIES
    CXX_STANDARD 20
    COMPILE_WARNING_AS_ERROR OFF 
)

# add local libraries here. NOTE: Local folder libraries must have a CMakeLists.txt
#add_subdirectory(include)

# Get system libraries to link
find_package(Vulkan REQUIRED)

# Get system libraries that can't be handled by find_package()
# syntax is: variable, folder library and file library, Absolute path of where the library install is
find_path(GLM_INCLUDE_DIR glm/glm.hpp
    PATHS "C:/VulkanSDK/1.3.296.0/Include"
    REQUIRED
)

# GLFW3 Example inclusion
find_path(GLFW_INCLUDE_DIR glfw/glfw3.h
    PATHS "C:/VulkanSDK/1.3.296.0/Include"
    REQUIRED
)


#Add include path for system libraries
target_include_directories(App PRIVATE ${GLM_INCLUDE_DIR} ${GLFW_INCLUDE_DIR})

# add libraries to link, name must match library folder name.
target_link_libraries(App PRIVATE Vulkan::Vulkan glm glfw)
