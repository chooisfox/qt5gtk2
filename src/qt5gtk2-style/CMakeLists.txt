add_library(qt5gtk2-style MODULE
    plugin.cpp
    qgtk2painter.cpp
    qgtkpainter.cpp
    qgtkstyle.cpp
    qgtkstyle_p.cpp
    qstylehelper.cpp
)

target_compile_definitions(qt5gtk2-style PRIVATE QT_NO_ANIMATION)

target_include_directories(qt5gtk2-style PRIVATE
    ${Qt5Core_PRIVATE_INCLUDE_DIRS}
    ${Qt5Gui_PRIVATE_INCLUDE_DIRS}
    ${Qt5Widgets_PRIVATE_INCLUDE_DIRS}
)

target_link_libraries(qt5gtk2-style PRIVATE
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    ${GTK2_LIBRARIES}
    ${X11_LIBRARIES}
)

set_target_properties(qt5gtk2-style PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/plugins/styles"
)

install(TARGETS qt5gtk2-style
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}/qt5/plugins/styles
)
install(FILES qt5gtk2.json
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/qt5/plugins/styles
)
