file(GLOB_RECURSE QML_SRCS *.qml *.js)

set(papyros-files_SRCS
    main.cpp
    ${QML_SRCS}
)

add_executable(papyros-files ${papyros-files_SRCS})

qt5_use_modules(papyros-files Gui Qml Quick)

if(NOT "${CMAKE_CURRENT_SOURCE_DIR}" STREQUAL "${CMAKE_CURRENT_BINARY_DIR}")
add_custom_target(papyros-files-qmlfiles ALL
    COMMAND cp -r ${CMAKE_CURRENT_SOURCE_DIR}/qml ${CMAKE_CURRENT_BINARY_DIR}
    DEPENDS ${QMLFILES}
)
endif(NOT "${CMAKE_CURRENT_SOURCE_DIR}" STREQUAL "${CMAKE_CURRENT_BINARY_DIR}")

install(DIRECTORY qml DESTINATION ${DATA_DIR})
install(TARGETS papyros-files RUNTIME DESTINATION bin)
