
cmake_minimum_required(VERSION 3.1)
# Disable in source builds
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

#####################################################################
# Project Stellar
#####################################################################
project(Stellar VERSION 1.0.0)

option(SINGLE "Use single precision" OFF)
option(STELLAR_SELF_CHECK "Compile Starbase with self-checks" OFF)
option(STELLAR_PARANOID "Compile Starbase in PARANOID mode" OFF)

set(TARGET_BINS "")
set(TARGET_LIBS "")
set(COMPILE_DEFS "")

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)

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