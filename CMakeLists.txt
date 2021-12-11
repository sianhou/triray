cmake_minimum_required(VERSION 3.0.0)
project(TRIRAY VERSION 0.1.0)

include(CTest)
enable_testing()

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

set(CMAKE_C_FLAGS "-DOVERRIDE_CWP_COMPLEX")

include_directories(cwp/include)
file(GLOB cwp_files "cwp/lib/*.c")
add_library(cwp ${cwp_files})

include_directories(par/include)
file(GLOB par_files "par/lib/*.c")
add_library(par ${par_files})

include_directories(Triangles/include)
file(GLOB tri_files "Triangles/lib/*.c")
add_library(tri ${tri_files})


add_executable(TRIRAY triray.c)
target_link_libraries(TRIRAY cwp)
target_link_libraries(TRIRAY par)
target_link_libraries(TRIRAY tri)