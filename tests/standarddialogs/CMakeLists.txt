add_executable(standarddialogs
    main.cpp
    dialog.cpp
)
target_link_libraries(standarddialogs PRIVATE Qt5::Widgets)

set(QT_PLUGIN_BUILD_PATH "${CMAKE_BINARY_DIR}/plugins")
configure_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/test.sh.in"
    "${CMAKE_CURRENT_BINARY_DIR}/test.sh"
    @ONLY
)
execute_process(COMMAND chmod +x "${CMAKE_CURRENT_BINARY_DIR}/test.sh")

add_test(
    NAME standarddialogs-test
    COMMAND "${CMAKE_CURRENT_BINARY_DIR}/test.sh"
    WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
)

install(TARGETS standarddialogs
    DESTINATION share/qt/examples/widgets/dialogs/standarddialogs
)
