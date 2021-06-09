cmake_minimum_required(VERSION 3.14)
project(foo C)

enable_testing()

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS TRUE)
set(BUILD_SHARED_LIBS TRUE)

add_subdirectory(lib)

add_executable(main main.c)
target_link_libraries(main PRIVATE addone)

add_test(NAME MissingDLL COMMAND $<TARGET_FILE:main>)
