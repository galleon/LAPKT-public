include_directories(${CMAKE_SOURCE_DIR}/interfaces/agnostic/ . ${Boost_INCLUDE_DIR} ${PYTHON_INCLUDE_DIRS})
add_library(pyagnostic SHARED py_strips_prob.cxx)
target_link_libraries(pyagnostic ${Boost_LIBRARIES})
install(TARGETS pyagnostic LIBRARY DESTINATION ${__dest})

