cmake_minimum_required(VERSION 3.7)
include(../../cmake/HermitCore-Application.cmake)

project(hermit_benchmarks C)

add_executable(basic basic.c)
target_link_libraries(basic pthread)

add_executable(hg hg.c hist.c rdtsc.c run.c init.c opt.c report.c setup.c)

if(NOT ${NO_NET})
add_executable(netio netio.c)
endif(NOT ${NO_NET})

if(NOT ${NO_IRCCE})
add_executable(RCCE_pingpong RCCE_pingpong.c)
target_link_libraries(RCCE_pingpong ircce)
endif(NOT ${NO_IRCCE})

add_executable(stream stream.c)
target_compile_options(stream PRIVATE -fopenmp)
target_link_libraries(stream -fopenmp)

add_subdirectory (ua.b)
add_subdirectory (cg.b)
add_subdirectory (ep.b)
add_subdirectory (bt.b)
add_subdirectory (is.b)
add_subdirectory (mg.b)
add_subdirectory (sp.b)

# deployment
install_local_targets(extra/benchmarks)
