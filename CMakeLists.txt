cmake_minimum_required(VERSION 3.5)
project(OpcUaTestServer)

set(CMAKE_VERBOSE_MAKEFILE ON)

add_subdirectory(open62541)

include_directories( ${PROJECT_SOURCE_DIR}/open62541/include/ ${CMAKE_CURRENT_BINARY_DIR}/src_generated/)
set(SOURCE_FILES main.c ${CMAKE_CURRENT_BINARY_DIR}/src_generated/open62541/namespace_OpcUaTestServer_generated.c)

set( open62541_TOOLS_DIR ${PROJECT_SOURCE_DIR}/open62541/tools)
set( open62541_NODESET_DIR ${PROJECT_SOURCE_DIR}/open62541/deps/ua-nodeset)

ua_generate_nodeset_and_datatypes(
    NAME "OpcUaTestServer"
    FILE_NS "${PROJECT_SOURCE_DIR}/nodeset/OpcUaTestServer.xml"
)

set(CMAKE_C_FLAGS "-std=c99")
add_executable(OpcUaTestServer ${SOURCE_FILES})
target_link_libraries(OpcUaTestServer open62541)
add_dependencies(OpcUaTestServer open62541-generator-ns-OpcUaTestServer)
