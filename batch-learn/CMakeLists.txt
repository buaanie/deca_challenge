cmake_minimum_required(VERSION 2.6)
project(batch-learn)

#set_target_properties(batch-learn PROPERTIES LINK_SEARCH_START_STATIC 1)
#set_target_properties(batch-learn PROPERTIES LINK_SEARCH_END_STATIC 1)
#set(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
#set(CMAKE_EXE_LINKER_FLAGS "-static-libgcc -static-libstdc++")


find_package(OpenMP REQUIRED)
find_package(Boost REQUIRED program_options)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")

include_directories(${Boost_INCLUDE_DIR})
link_directories(${Boost_LIBRARY_DIRS})

file(GLOB SRCS src/*.cpp src/**/*.cpp)
include_directories(include)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -O3 -std=c++11 -march=native")

SET(CMAKE_FIND_LIBRARY_SUFFIXES ".a")
SET(BUILD_SHARED_LIBRARIES OFF)
SET(CMAKE_EXE_LINKER_FLAGS "-static")
add_executable(${PROJECT_NAME} ${SRCS})
set_target_properties(${PROJECT_NAME} PROPERTIES LINK_SEARCH_START_STATIC 1)
set_target_properties(${PROJECT_NAME} PROPERTIES LINK_SEARCH_END_STATIC 1)
target_link_libraries(${PROJECT_NAME} -static-libgcc -static-libstdc++ boost_program_options)
