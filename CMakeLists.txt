cmake_minimum_required(VERSION 3.24)
project(chapter1-basics LANGUAGES CXX)

set(CMAKE_AUTOMOC ON)

find_package(Qt6 REQUIRED COMPONENTS Core Gui Qml Quick)

## Make the QML modules known in the subdirectory. See for more information also
## https://doc.qt.io/qtcreator/creator-qml-modules-with-plugins.html#importing-qml-modules
set(QML_IMPORT_PATH "${CMAKE_SOURCE_DIR}/qml" CACHE STRING "Additional QML import paths" FORCE)

add_subdirectory(qml/MyQuick)

qt_add_executable(${PROJECT_NAME}
    main.cpp
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    WIN32_EXECUTABLE TRUE
    MACOSX_BUNDLE TRUE
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        MyQuickModuleplugin
    PUBLIC
        Qt::Quick
        Qt::Gui
        Qt::Qml
        Qt::Core
)

target_include_directories(${PROJECT_NAME}
    PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/qml/MyQuick")

qt_add_qml_module(${PROJECT_NAME}
    URI Charts
    VERSION 1.0
    QML_FILES
        ChartItem.qml
    NO_RESOURCE_TARGET_PATH
    DEPENDENCIES QtQuick
)

install(TARGETS ${PROJECT_NAME}
    RUNTIME DESTINATION "bin"
    BUNDLE DESTINATION "bin"
    LIBRARY DESTINATION "lib"
)
