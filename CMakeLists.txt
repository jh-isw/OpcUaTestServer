cmake_minimum_required(VERSION 3.5)
project(OpcUaTestServer)

set(CMAKE_VERBOSE_MAKEFILE ON)

add_subdirectory(open62541)

set(SOURCE_FILES main.c)

set(CMAKE_C_FLAGS "-std=c99")
#set(CMAKE_CXX_STANDARD 11)
add_executable(OpcUaTestServer ${SOURCE_FILES})
target_link_libraries(OpcUaTestServer open62541)
