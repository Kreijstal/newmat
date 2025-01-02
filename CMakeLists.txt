cmake_minimum_required(VERSION 3.10)
project(newmat VERSION 1.10.4)
option(USE_NAMESPACE "Compile with -Duse_namespace" OFF)

# Set C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Compiler flags
add_compile_options(-Wall -Wextra -pedantic)

# Collect all header files
file(GLOB_RECURSE HEADERS "*.h")

# Collect all source files for the library
file(GLOB_RECURSE SOURCES "*.cpp" "*.c")

# Exclude source files for executables
list(REMOVE_ITEM SOURCES
    "${CMAKE_CURRENT_SOURCE_DIR}/example.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/test_exc.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt1.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt2.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt3.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt4.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt5.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt6.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt7.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt8.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmt9.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmta.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtb.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtc.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtd.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmte.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtf.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtg.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmth.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmti.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtj.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtk.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtl.cpp"
    "${CMAKE_CURRENT_SOURCE_DIR}/tmtm.cpp"
)

# Define the library
add_library(newmat ${SOURCES} ${HEADERS})

if (USE_NAMESPACE)
    target_compile_definitions(newmat PUBLIC -Duse_namespace)
endif()

# Include directories
target_include_directories(newmat PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include/newmat>
)

# Define the example executable
add_executable(example example.cpp)
target_link_libraries(example newmat)

# Define the test_exc executable
add_executable(test_exc test_exc.cpp)
target_link_libraries(test_exc newmat)

# Define the tmt executable
add_executable(tmt tmt.cpp tmt1.cpp tmt2.cpp tmt3.cpp tmt4.cpp tmt5.cpp tmt6.cpp tmt7.cpp tmt8.cpp tmt9.cpp tmta.cpp tmtb.cpp tmtc.cpp tmtd.cpp tmte.cpp tmtf.cpp tmtg.cpp tmth.cpp tmti.cpp tmtj.cpp tmtk.cpp tmtl.cpp tmtm.cpp)
target_link_libraries(tmt newmat)

# Install the library
install(TARGETS newmat DESTINATION lib)

# Install the headers
install(FILES ${HEADERS} DESTINATION include/newmat)
