cmake_minimum_required(VERSION 3.24)
project(MyQuickModule LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Qml Quick)

qt_add_library(${PROJECT_NAME} STATIC)
qt_add_qml_module(${PROJECT_NAME}
    URI MyQuick
    VERSION 1.0
    SOURCES
        piechart.h
        piechart.cpp
    DEPENDENCIES QtQuick
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE Qt6::Quick)

target_include_directories(${PROJECT_NAME}
    PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
