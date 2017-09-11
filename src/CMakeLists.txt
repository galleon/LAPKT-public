add_definitions("-O3 -Wall -std=c++0x -DNDEBUG")
add_library(aptk SHARED bit_array.cxx bit_set.cxx memory.cxx)
install(TARGETS aptk DESTINATION ${__dest})

