find_package(Vulkan REQUIRED)

# Engine library target
file(GLOB_RECURSE ENGINE_SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp"
)

add_library(engine_lib STATIC ${ENGINE_SOURCES})

# Include dirs
target_include_directories(engine_lib
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/include
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/src
)

# Link dependencies
target_link_libraries(engine_lib
    PUBLIC
        Vulkan::Vulkan
)

# Compiler features and definitions
target_compile_features(engine_lib PUBLIC cxx_std_20)

target_compile_definitions(engine_lib PRIVATE
    $<$<CONFIG:Debug>:ME_DEBUG>
    $<$<CONFIG:Release>:ME_RELEASE>
    $<$<PLATFORM_ID:Darwin>:ME_PLATFORM_MAC>
    $<$<PLATFORM_ID:Windows>:ME_PLATFORM_WINDOWS>
    $<$<PLATFORM_ID:Linux>:ME_PLATFORM_LINUX>
)

# Compile commands symlink for clangd
if(CMAKE_EXPORT_COMPILE_COMMANDS)
    execute_process(
        COMMAND ${CMAKE_COMMAND} -E create_symlink
            ${CMAKE_BINARY_DIR}/compile_commands.json
            ${CMAKE_SOURCE_DIR}/compile_commands.json   
    )
endif()