include(FetchContent)
set(SFML_VERSION "2.5.1")

FetchContent_Declare(
    sfml
    GIT_REPOSITORY "https://github.com/SFML/SFML.git"
    GIT_TAG        "${SFML_VERSION}"
)

FetchContent_GetProperties(sfml)
if(NOT sfml_POPULATED)
    FetchContent_Populate(sfml)
    add_subdirectory(${sfml_SOURCE_DIR} ${sfml_BINARY_DIR})
endif()
FetchContent_MakeAvailable(sfml)

message("A: ${sfml_SOURCE_DIR}")
include_directories(${sfml_SOURCE_DIR}/include)
find_package(OpenCV REQUIRED)

add_executable(
    Pixelsona
        main.cpp
)


target_link_libraries(
    Pixelsona
      PRIVATE
        sfml-audio
        sfml-graphics
        sfml-system
        sfml-window
)

if (WIN32 AND BUILD_SHARED_LIBS)
    add_custom_command(
        TARGET
            Pixelsona
        POST_BUILD
            COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:Pixelsona> $<TARGET_FILE_DIR:Pixelsona> COMMAND_EXPAND_LISTS)
endif()

set_target_properties( 
    Pixelsona
      PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${PIXELSONA_BIN_DIR}"
)

install(TARGETS ${PROJECT_NAME} DESTINATION ${PIXELSONA_BIN_DIR})