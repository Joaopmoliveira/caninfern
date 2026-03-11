add_executable(crbruscomp compiler.cpp)
target_link_libraries(crbruscomp PRIVATE nlohmann_json::nlohmann_json)
