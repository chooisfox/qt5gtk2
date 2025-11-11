add_library(qt5gtk2 MODULE
    main.cpp
    qt5gtk2theme.cpp
    qt5gtk2dialoghelpers.cpp
)

target_include_directories(qt5gtk2 PRIVATE
    ${Qt5Core_PRIVATE_INCLUDE_DIRS}
    ${Qt5Gui_PRIVATE_INCLUDE_DIRS}
    ${Qt5ThemeSupport}
)

target_link_libraries(qt5gtk2 PRIVATE
    Qt5::Core
    Qt5::Gui
    ${GTK2_LIBRARIES}
    ${X11_LIBRARIES}
)

if(Qt5_VERSION_MINOR GREATER 7)
    find_package(Qt5 5.7.0 REQUIRED COMPONENTS ThemeSupport)
    message(STATUS "Qt > 5.7: Using Gui (for ThemeSupport) private headers")
    target_include_directories(qt5gtk2 PRIVATE ${Qt5ThemeSupport_PRIVATE_INCLUDE_DIRS})
    target_link_libraries(qt5gtk2 PRIVATE Qt5::ThemeSupport)
else()
    find_package(Qt5 5.7.0 REQUIRED COMPONENTS PlatformSupport)
    message(STATUS "Qt <= 5.7: Using PlatformSupport private headers and library")
    target_include_directories(qt5gtk2 PRIVATE ${Qt5PlatformSupport_PRIVATE_INCLUDE_DIRS})
    target_link_libraries(qt5gtk2 PRIVATE Qt5::PlatformSupport)
endif()

set_target_properties(qt5gtk2 PROPERTIES
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/plugins/platformthemes"
)

install(TARGETS qt5gtk2
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}/qt5/plugins/platformthemes
)
install(FILES qt5gtk2.json
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/qt5/plugins/platformthemes
)
