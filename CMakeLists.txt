cmake_minimum_required(VERSION 3.8.2)

project(rnnlmlib VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find includes in the build directories
set(CMAKE_INCLUDE_CURRENT_DIR ON)


set(HEADERS
    include/fastexp.h
    include/rnnlmlib.h
)

set(SRCS
    src/rnnlmlib.cpp
)

# Tell CMake to create the helloworld executable
add_library(rnnlmlib ${SRCS} ${HEADERS})

include_directories(include)

export(TARGETS rnnlmlib NAMESPACE rnnlmlib:: FILE rnnlmlibTargets.cmake)

install(TARGETS rnnlmlib
    EXPORT rnnlmlibTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include
)

install(FILES ${HEADER} DESTINATION include)

install(DIRECTORY include/
        DESTINATION include/)
        
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    rnnlmlibConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
)

install(EXPORT rnnlmlibTargets
        FILE rnnlmlibTargets.cmake
        NAMESPACE rnnlmlib::
        DESTINATION lib/cmake/rnnlmlib
)

configure_file(rnnlmlibConfig.cmake.in rnnlmlibConfig.cmake @ONLY)