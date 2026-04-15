# Game executable
add_executable(game
    src/main.cpp
)

# Link against engine
target_link_libraries(game
    PRIVATE
        engine_lib
)

# Compiler features
target_compile_features(game PRIVATE cxx_std_20)