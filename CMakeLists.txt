cmake_minimum_required(VERSION 3.20)

project(project_name.elf VERSION 0.0.1 LANGUAGES CXX)

find_package(libhal-lpc40xx REQUIRED CONFIG)

add_executable(${PROJECT_NAME} main.cpp newlib.cpp)
target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)
target_include_directories(${PROJECT_NAME} PUBLIC .)
target_compile_options(${PROJECT_NAME} PRIVATE ${CORTEX_M4F_FLAGS})
target_link_options(${PROJECT_NAME} PRIVATE -T libhal-lpc40xx/lpc4078.ld)
target_link_libraries(${PROJECT_NAME} PRIVATE libhal::lpc40xx)
arm_cortex_post_build(${PROJECT_NAME})