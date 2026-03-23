cmake_minimum_required(VERSION 3.20)
project(RedPlasmaKernel VERSION 0.1.0 LANGUAGES C CXX)

# ⚖️ License: Mozilla Public License 2.0 (See LICENSE file)
# This project scales from 16-bit to modern Linux workstations.

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 🏗️ Rule 2: Architecture & Sandboxing
# Ensuring the Kernel stays "Blind" to specific hardware implementations.
include_directories(include)

# 📂 Define Source Files
set(KERNEL_SOURCES
        src/main.cpp
        include/rp_types.h
)

# 🚀 Build the Heartbeat
add_executable(RedPlasmaKernel ${KERNEL_SOURCES})

# 🛠️ Fedora Dependencies (Wayland/Vulkan for future plugin support)
# Note: The Kernel remains "Blind" but we ensure the environment is ready.
find_package(PkgConfig REQUIRED)
# pkg_check_modules(WAYLAND REQUIRED wayland-client)

# 📍 Rule 3: Evolutionary Calibration Output
# Ensure the build directory has a place for plugins
add_custom_command(TARGET RedPlasmaKernel POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E make_directory ${CMAKE_BINARY_DIR}/plugins
        COMMENT "Creating the Plugin Sandbox..."
)