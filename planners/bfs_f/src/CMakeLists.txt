include_directories(${CMAKE_SOURCE_DIR}/interfaces/agnostic/ ${CMAKE_SOURCE_DIR}/planners/python/agnostic/ . ${Boost_INCLUDE_DIR} ${PYTHON_INCLUDE_DIRS})
add_library(bfsf SHARED bfsf_planner.cxx module.cxx)
target_link_libraries(bfsf aptk pyagnostic agnostic ${Boost_LIBRARIES})
install(TARGETS fsf DESTINATION ${__dest})
