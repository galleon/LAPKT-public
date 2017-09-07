CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

find_package(PythonLibs REQUIRED)

message (WARNING "PYTHONLIBS_VERSION_STRING: ${PYTHONLIBS_VERSION_STRING}")
message (WARNING "PYTHON_VERSION_MAJOR: ${PYTHON_VERSION_MAJOR}")

#if (${PYTHON_VERSION_MAJOR} EQUAL 3)
#  find_package(Boost COMPONENTS python3)
#else()
#  find_package(Boost COMPONENTS python)
#endif()
#
find_package(Boost 1.61)
#
find_package(Boost COMPONENTS python REQUIRED)
#
# Add BOOST & PYTHON include
#
include_directories(${Boost_INCLUDE_DIR} ${PYTHON_INCLUDE_DIRS})
#
# aptk is in include
#
include_directories(include planners/python/agnostic/ interfaces/agnostic/)

if(CMAKE_COMPILER_IS_GNUCXX)
  add_definitions("-O3 -Wall -std=c++0x -DNDEBUG")
else()
  message(FATAL_ERROR "CMakeLists.txt has not been tested/written for your compiler.")
endif()

add_subdirectory(planners/bfs_f/src)

#set(CORELIBS ${Boost_LIBRARIES} ${PYTHON_LIBRARIES})

#add_library(demo SHARED ./main.cpp)
#target_link_libraries(demo ${CORELIBS})
