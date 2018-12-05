
cmake_minimum_required(VERSION 3.1)
# Disable in source builds
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

#####################################################################
# Project Stellar
#####################################################################
project(Stellar VERSION 1.0.0)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

# if(WIN32)
#     set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)
# endif()

add_library(Starbase STATIC "src/Starbase.c" "src/Starbase.h")
target_compile_definitions(Starbase PRIVATE NOMAIN)

list(APPEND SOURCES
    "src/anisotropy.c"
    "src/arraypoolstack.c"
    "src/classify.c"
    "src/improve.c"
    "src/insertion.c"
    "src/interact.c"
    "src/journal.c"
    "src/main.c"
    "src/output.c"
    "src/print.c"
    "src/quadric.c"
    "src/quality.c"
    "src/size.c"
    "src/smoothing.c"
    "src/top.c"
    "src/topological.c"
    "src/vector.c"
)

add_executable(Stellar src/Stellar.c)
target_sources(Stellar PRIVATE ${SOURCES})

target_link_libraries(Stellar Starbase)