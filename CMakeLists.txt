cmake_minimum_required(VERSION 3.16)

project(qtcmake VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find required Qt modules
find_package(Qt6 REQUIRED COMPONENTS Quick)

# Standard Qt project setup (handles warnings, rpaths, etc.)
qt_standard_project_setup(REQUIRES 6.8)

# Define the executable target
qt_add_executable(appqtcmake
    main.cpp
)

# Add QML module (no local paths needed)
qt_add_qml_module(appqtcmake
    URI qtcmake
    VERSION 1.0
    QML_FILES Main.qml
)

# Set platform-specific properties
set_target_properties(appqtcmake PROPERTIES
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    # MACOSX_BUNDLE_GUI_IDENTIFIER com.example.appqtcmake
)

# Link Qt libraries
target_link_libraries(appqtcmake PRIVATE Qt6::Quick)

# Install rules (no hardcoded paths)
include(GNUInstallDirs)
install(TARGETS appqtcmake
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
