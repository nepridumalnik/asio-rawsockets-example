cmake_minimum_required(VERSION 3.12)
project(asio-rawsockets-example)

# Bypass _WIN32_WINNT warn
if(WIN32)
    macro(get_WIN32_WINNT version)
        if (WIN32 AND CMAKE_SYSTEM_VERSION)
            set(ver ${CMAKE_SYSTEM_VERSION})
            string(REPLACE "." "" ver ${ver})
            string(REGEX REPLACE "([0-9])" "0\\1" ver ${ver})
            set(${version} "0x${ver}")
        endif()
    endmacro()
    get_WIN32_WINNT(ver)
    add_definitions(-D_WIN32_WINNT=${ver})
endif()

set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 14)

find_package(Boost REQUIRED system)

include_directories(${Boost_INCLUDE_DIRS})

add_executable(example ${CMAKE_CURRENT_SOURCE_DIR}/src/example.cpp)
target_include_directories(example PUBLIC ${Boost_INCLUDE_DIR})
target_link_libraries(example PUBLIC ${Boost_LIBRARIES})
