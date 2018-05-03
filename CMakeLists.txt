cmake_minimum_required(VERSION 2.8.12)
project(Trojan)
option(STATIC "STATIC")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3")
set(THREADS_PREFER_PTHREAD_FLAG ON)

set(Boost_USE_STATIC_LIBS ON)

add_executable(trojan src/clientsession.cpp src/config.cpp src/log.cpp src/main.cpp src/serversession.cpp src/service.cpp src/session.cpp src/socks5address.cpp src/ssldefaults.cpp src/trojanrequest.cpp src/udppacket.cpp src/version.cpp)
find_package(Threads REQUIRED)
target_link_libraries(trojan ${CMAKE_THREAD_LIBS_INIT})

find_package(Boost 1.54.0 REQUIRED COMPONENTS system)
include_directories(${Boost_INCLUDE_DIR})
target_link_libraries(trojan ${Boost_LIBRARIES})
find_package(OpenSSL 1.0.2 REQUIRED)
include_directories(${OPENSSL_INCLUDE_DIR})
target_link_libraries(trojan ${OPENSSL_LIBRARIES})

    target_link_libraries(trojan wsock32 ws2_32)
    if (STATIC)
        target_link_libraries(trojan -static)
    endif()
