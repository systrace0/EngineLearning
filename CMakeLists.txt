cmake_minimum_required(VERSION 3.24...4.0)

project(MyEngine
    VERSION 0.1.0
    DESCRIPTION "Vulkan Game Engine"
    LANGUAGES CXX
)

# Global CMake settings
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Build type default
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug CACHE STRING "Build type" FORCE)
endif()

# vcpkg
if(DEFINED ENV{VCPKG_ROOT} AND NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    set(CMAKE_TOOLCHAIN_FILE "$ENV{VCPKG_ROOT}/sscripts/buildsystems/vcpkg.cmake"
        CACHE STRING "CMake toolchain file")
endif()

# subdirs
add_subdirectory(engine)
add_subdirectory(game)