cmake_minimum_required(VERSION 3.16)
project("pybind11you")
set(CMAKE_CXX_STANDARD 17)

set(APP_SOURCE "${PROJECT_SOURCE_DIR}/source/app")
set(MODULE_SOURCE "${PROJECT_SOURCE_DIR}/source/module")
set(EXTERNALS "${PROJECT_SOURCE_DIR}/externals")
set(EIGEN_DIR "C:\\Eigen\\")

# pybind11
add_subdirectory(${EXTERNALS}/pybind11)
include_directories(${EIGEN_DIR})

# module
pybind11_add_module (
    custom_functions 
    ${MODULE_SOURCE}/module.cpp
)

target_include_directories (
    custom_functions 
    PRIVATE ${MODULE_SOURCE}
)

# app
add_executable (
    pybind11app
    ${APP_SOURCE}/app.cpp
)

target_include_directories (
    pybind11app 
    PRIVATE ${APP_SOURCE}
    PRIVATE ${MODULE_SOURCE}
)

target_link_libraries(
    pybind11app
    PRIVATE pybind11::embed
)

