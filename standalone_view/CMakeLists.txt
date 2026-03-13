find_package(PkgConfig REQUIRED)

# Try to find GLFW using different methods
pkg_check_modules(GLFW REQUIRED IMPORTED_TARGET glfw3)


add_executable(sceneviewer
    glfwviewer.cpp
)
target_link_libraries(sceneviewer
    PUBLIC 
        PkgConfig::GLFW
        wescene-renderer
)

if(BUILD_QML)
    find_package(Qt6 COMPONENTS Qml Quick REQUIRED)

    set(CMAKE_AUTOMOC ON) 
    set(CMAKE_AUTORCC ON) 
    set(CMAKE_AUTOUIC ON)

    add_executable(sceneviewer-qml
        qmlviewer.cpp
        main.qml
        pkg.qrc
    )
    target_link_libraries(sceneviewer-qml
        PUBLIC 
        Qt6::Qml
        Qt6::Quick
        wescene-renderer-qml
    )
    set(CMAKE_AUTOMOC OFF) 
    set(CMAKE_AUTORCC OFF) 
    set(CMAKE_AUTOUIC OFF)
endif()
