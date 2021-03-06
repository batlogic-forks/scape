project(qtEditor)

set(CMAKE_DEBUG_POSTFIX "_d")
set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/bin")

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

set(SRC_FILES
./main.cpp
./MainWindow.cpp
./OgreWidget.cpp
./StartupSettingsDialog.cpp
./AboutDialog.cpp
./PropertiesWidget.cpp
./PresetsWidget.cpp
./ImageFileDialog.cpp
./ImportImageDialog.cpp
./ExportImageDialog.cpp
./BrushSettingsWidget.cpp
./ButtonDefinitionDetailsDialog.cpp
./ButtonDefinitionsDialog.cpp
)

set(HEADER_FILES
./MainWindow.h
./OgreWidget.h
./StartupSettingsDialog.h
./AboutDialog.h
./PropertiesWidget.h
./PresetsWidget.h
./ImageFileDialog.h
./ImportImageDialog.h
./ExportImageDialog.h
./BrushSettingsWidget.h
./ButtonDefinitionDetailsDialog.h
./ButtonDefinitionsDialog.h
)

set(RESOURCE_SRCS ./res/editor.qrc)

if(WIN32)
        file(GLOB RES ./res/*.rc)
        set(RESOURCE_SRCS ${RESOURCE_SRCS} ${RES})
endif(WIN32)

configure_file(./ScapeVersion.h.in ${CMAKE_CURRENT_BINARY_DIR}/ScapeVersion.h @ONLY)

add_executable(qtEditor WIN32
    ${HEADER_FILES}
    ${SRC_FILES}
    ${RESOURCE_SRCS}
)

target_include_directories(qtEditor PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

set_target_properties(qtEditor PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/$<0:>")

if(WIN32)
    set_target_properties(qtEditor PROPERTIES DEBUG_POSTFIX _d)
    set_property(TARGET qtEditor PROPERTY WIN32_EXECUTABLE 0)
endif()

target_link_libraries(qtEditor
    ${OGRE_LIBRARIES}
    Qt5::Gui
    Qt5::Core
    Qt5::Widgets
    Engine
)

