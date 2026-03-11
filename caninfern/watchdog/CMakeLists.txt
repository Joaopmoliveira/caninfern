add_library(watchdoginterface INTERFACE)
target_include_directories(watchdoginterface INTERFACE ${CMAKE_CURRENT_LIST_DIR})

add_executable(watchdog watchdog.cpp)
target_link_libraries(watchdog PRIVATE 
asio 
watchdoginterface
)
