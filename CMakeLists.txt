cmake_minimum_required(VERSION 3.10.0)

project(raytracing)

# using Clang (linux or apple) or GCC
message("Using clang/gcc compiler flags")
SET(BASE_CXX_FLAGS "-std=c++11 -Wall -Wextra -Werror")
SET(DISABLED_WARNINGS " -Wno-unused-parameter -Wno-unused-variable -Wno-unused-function -Wno-deprecated-declarations -Wno-missing-braces -Wno-unused-private-field")
SET(TRACE_INCLUDES " -H -Wno-error=unused-command-line-argument")

if ("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang")
message("Setting clang-specific options")
SET(BASE_CXX_FLAGS "${BASE_CXX_FLAGS} -ferror-limit=3 -fcolor-diagnostics")
SET(CMAKE_CXX_FLAGS_DEBUG          "-g3 -fsanitize=address -fno-limit-debug-info")
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
message("Setting gcc-specific options")
SET(BASE_CXX_FLAGS "${BASE_CXX_FLAGS} -fmax-errors=5")
SET(CMAKE_CXX_FLAGS_DEBUG          "-g3")
SET(DISABLED_WARNINGS "${DISABLED_WARNINGS} -Wno-maybe-uninitialized -Wno-format-zero-length -Wno-unused-but-set-parameter -Wno-unused-but-set-variable")
endif()

SET(CMAKE_CXX_FLAGS "${BASE_CXX_FLAGS} ${DISABLED_WARNINGS}")
SET(CMAKE_CXX_FLAGS_RELEASE        "-O3 -march=native -DNDEBUG")

add_executable(raytracing src/main.cc)