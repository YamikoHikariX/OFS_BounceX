cmake_minimum_required(VERSION 3.16)

# Add this before any add_subdirectory calls
set(CMAKE_POLICY_DEFAULT_CMP0048 NEW)
# Add this line to force minimum version for all subdirectories
set(CMAKE_POLICY_VERSION_MINIMUM 3.5)

project(scripter)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin")

# =============
# == OPTIONS ==
# =============
option(OFS_PROFILE OFF)
option(OFS_AVX OFF)

if(WIN32)
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
    if(OFS_AVX) 
        message("OFS AVX ENABLED")
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /arch:AVX")
    endif()
endif()

# ====================
# === DEPENDENCIES ===
# ====================
add_subdirectory("lib/")

# =====================
# ==== BUILD-TOOLS ====
# =====================
add_subdirectory("localization/")

# ==============
# ==== SRC ====
# ==============
add_subdirectory("OFS-lib/")
add_subdirectory("src/")

