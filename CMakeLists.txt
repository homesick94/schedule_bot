cmake_minimum_required(VERSION 2.8.4)
project(schedule_bot)

# Libs check and its params initialization
find_package(Threads REQUIRED)
find_package(OpenSSL REQUIRED)
find_package(Boost COMPONENTS system iostreams date_time REQUIRED)
set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)

# Set project params
set(EXECUTABLE schedule_bot)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++1y -W -Wall -Wcast-align -pedantic -fstack-protector-all -Wfloat-equal -Wpointer-arith -Wwrite-strings -Wcast-align -Wno-format -Wno-long-long -Wmissing-declarations -Wno-unused-function")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Ofast")

# Source files list
set(SOURCES_LIST src/main.cpp
                 src/user.cpp
                 src/event.cpp
                 src/report_system.cpp
                 src/sch_bot.cpp
                 src/schedule.cpp
                 src/notifies.cpp)

# Headers directories list
set(HEADERS_DIRS_LIST ./src/include ./config)

add_executable(${EXECUTABLE} ${SOURCES_LIST})
include_directories(${HEADERS_DIRS_LIST} /usr/local/include ${OPENSSL_INCLUDE_DIR} ${Boost_INCLUDE_DIR})
target_link_libraries(${EXECUTABLE} /usr/local/lib/libTgBot.a ${CMAKE_THREAD_LIBS_INIT} ${OPENSSL_LIBRARIES} ${Boost_LIBRARIES})
