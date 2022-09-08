cmake_minimum_required(VERSION 3.10)

project("uv_link" LANGUAGES C)

add_library(uv_link OBJECT
        src/uv_link_t.c
        src/uv_link_source_t.c
        src/uv_link_observer_t.c
        src/defaults.c
)

set_target_properties(uv_link
        PROPERTIES
        C_STANDARD 99
)

target_include_directories(uv_link
        PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        PRIVATE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)

if(HAVE_LIBUV)
        set(LIBUV_NAME uv)
else()
        set(LIBUV_NAME uv_a)
endif()

target_link_libraries(uv_link PUBLIC ${LIBUV_NAME})