
cmake_minimum_required(VERSION 3.1)
project(C_MAKE_DEMO)

if(APPLE)
    # no warning
    # https://stackoverflow.com/questions/31561309/cmake-warnings-under-os-x-macosx-rpath-is-not-specified-for-the-following-targe
    set(CMAKE_MACOSX_RPATH 0)
endif()

set(BINARY_NAME extern_test)

set(c_common ${CMAKE_CURRENT_LIST_DIR}/../../GitHub/c_cpp_common)

set(Source_files 
	#${CMAKE_CURRENT_SOURCE_DIR}/main.cpp
	${CMAKE_CURRENT_SOURCE_DIR}/common.h
    ${CMAKE_CURRENT_LIST_DIR}/cfuhash.c
    ${CMAKE_CURRENT_LIST_DIR}/cfuhash.h
    ${CMAKE_CURRENT_LIST_DIR}/hash_usage.c

    ${c_common}/crt_dbg_leak.c
    ${c_common}/crt_dbg_leak.h
	)

add_executable(${BINARY_NAME} ${Source_files})
target_include_directories(${BINARY_NAME} PRIVATE ${c_common})
source_group(files FILES ${Source_files})

if(WIN32)
	target_compile_options(${BINARY_NAME} PRIVATE /source-charset:utf-8 /execution-charset:utf-8)
endif()
