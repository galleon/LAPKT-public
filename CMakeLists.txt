# Disable in-source builds to prevent source tree corruption.
if(" ${CMAKE_SOURCE_DIR}" STREQUAL " ${CMAKE_BINARY_DIR}")
  message(FATAL_ERROR "
FATAL: In-source builds are not allowed.
       You should create a separate directory for build files.
")
endif()

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
#include_directories(${Boost_INCLUDE_DIR} ${PYTHON_INCLUDE_DIRS})
#
# aptk is C++ and is located in src & include [Should we create a lib?]
# interfaces/agnostic/ contains only C++ [Should we create a lib?]
# planners/python/agnostic
#
include_directories(include)

if(CMAKE_COMPILER_IS_GNUCXX)
  add_definitions("-O3 -Wall -std=c++0x -DNDEBUG")
else()
  message(FATAL_ERROR "CMakeLists.txt has not been tested/written for your compiler.")
endif()

add_subdirectory(src)
add_subdirectory(interfaces/agnostic)
#
add_subdirectory(planners/python/agnostic)
add_subdirectory(planners/bfs_f/src)

# ICI JE CHERCHE A COPIER MES FICHIERS POUR EVENTUELLEMENT CREER MON MODULE

set(PYTHON_INSTALL_CONFIGURATIONS "")
set(__dst "${PYTHON_PACKAGES_PATH}")

if(NOT __dst)
  if(DEFINED ${PYTHON}_VERSION_MAJOR)
    set(__ver "${${PYTHON}_VERSION_MAJOR}.${${PYTHON}_VERSION_MINOR}")
  elseif(DEFINED ${PYTHON}_VERSION_STRING)
    set(__ver "${${PYTHON}_VERSION_STRING}")
  else()
    set(__ver "unknown")
  endif()
  if(INSTALL_CREATE_DISTRIB)
    set(__dst "python/${__ver}/${OpenCV_ARCH}")
  else()
    set(__dst "python/${__ver}")
  endif()
endif()

install(TARGETS ${the_module}
 ${PYTHON_INSTALL_CONFIGURATIONS}
 RUNTIME DESTINATION "${__dst}" COMPONENT python
 LIBRARY DESTINATION "${__dst}" COMPONENT python
 ${PYTHON_INSTALL_ARCHIVE}
)
