add_executable(sandbox
    main.cpp
)

target_link_libraries(sandbox PRIVATE engine_lib)
target_compile_features(sandbox PRIVATE cxx_std_20)