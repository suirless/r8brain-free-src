cmake_minimum_required(VERSION 3.16)
project(R8Brain C CXX)

option(BUILD_STATIC "Build R8Brain in static mode." OFF)

file(GLOB R8BRAIN_SRC
	"${CMAKE_CURRENT_SOURCE_DIR}/*.cpp"
	"${CMAKE_CURRENT_SOURCE_DIR}/*.h"
)

if (WIN32)
	SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
else()
	SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fPIC")
endif()

if (BUILD_STATIC)
    add_library(r8brain STATIC ${R8BRAIN_SRC})
else()
    add_library(r8brain SHARED ${R8BRAIN_SRC})
endif()

if (BUILD_ENABLE_XBOX)
    fresponze_create_xbox_target(r8brain)
endif()

target_include_directories(r8brain PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
