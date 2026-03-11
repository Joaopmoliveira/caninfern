add_executable(controller controller.cpp)
target_link_libraries(controller PRIVATE 
asio
watchdoginterface
)
