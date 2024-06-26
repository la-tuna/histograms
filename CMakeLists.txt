CMAKE_MINIMUM_REQUIRED(VERSION 3.17)
PROJECT(Histogram VERSION 0.1 LANGUAGES CXX)

set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set_property(GLOBAL PROPERTY PREDEFINED_TARGETS_FOLDER "cmake")
include(cmake/build_prefix.cmake)

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")

SET(APP_NAME ${PROJECT_NAME})

set(CMAKE_MODULE_PATH
        ${CMAKE_MODULE_PATH}
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

SET(OPENCV_PROJECT_PATH CACHE STRING "Path to OpenCV directory.")
LIST(APPEND CMAKE_PREFIX_PATH ${OPENCV_PROJECT_PATH})

find_package(Doxygen)
IF (DOXYGEN_FOUND)
    add_subdirectory(doc)
endif ()

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

SET(SRC_DIR "${CMAKE_CURRENT_SOURCE_DIR}/src")

add_subdirectory(src)

ADD_EXECUTABLE(${PROJECT_NAME} main.cpp)
target_link_libraries(${PROJECT_NAME} Histogram_lib)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
