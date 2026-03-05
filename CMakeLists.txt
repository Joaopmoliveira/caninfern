project(caninfern)

# caninfern is heavily dependent on ASIO. Hence we directly include it as a
# system dependency
add_subdirectory(third_party)

# the compiler takes a json file and generates a memory layout in the shared memory space. 
# This makes our life substantially simpler.
add_subdirectory(compiler)

# this is where the three headed implementation of caninfern is located
add_subdirectory(caninfern)



