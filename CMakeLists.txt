cmake_minimum_required(VERSION 3.14)
project(Layman LANGUAGES CXX)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# Layman library
add_library(Layman
    src/layman.cpp
    src/layman.h
)
target_include_directories(Layman PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Sandbox executable
add_executable(sandbox
    sandbox/sandbox.cpp
)
target_link_libraries(sandbox PRIVATE Layman)
target_include_directories(sandbox PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Install rules (optional)
install(TARGETS Layman DESTINATION lib)
install(DIRECTORY include/ DESTINATION include)

# Set build directory to layman/build
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/build/lib)
