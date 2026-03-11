add_executable(crbruscomp compiler.cpp)
target_link_libraries(crbruscomp PRIVATE nlohmann_json::nlohmann_json)


# the compiler is very special, he needs to run, whenever a change is detected on the file sharedmemory
add_custom_command(
    OUTPUT Byproducts
    COMMAND SharedMemoryCompiler "${CMAKE_CURRENT_LIST_DIR}/sharedmemory.json"
    DEPENDS SharedMemoryCompiler
    COMMENT "currently compiling shared memory layout from sharedmemory.json"
    )

# create a target that includes some_file, this gives us a name that we can use later
add_custom_target(
    CompilerByproducts
  DEPENDS Byproducts
)

add_custom_command(
    OUTPUT CopyByproducts
    COMMAND ${CMAKE_COMMAND} -E copy 
                ${CMAKE_BINARY_DIR}/header_creator.h
                ${CMAKE_CURRENT_LIST_DIR}/header_creator.h
    COMMAND ${CMAKE_COMMAND} -E copy 
                ${CMAKE_BINARY_DIR}/header_acessor.h
                ${CMAKE_CURRENT_LIST_DIR}/header_acessor.h
    DEPENDS CompilerByproducts
    COMMENT "currently copying compiled shared memory layout"
    )

# create a target that includes some_file, this gives us a name that we can use later
add_custom_target(
    ByproductsCopy
  DEPENDS CopyByproducts
)

