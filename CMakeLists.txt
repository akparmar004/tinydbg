cmake_minimum_required (VERSION 3.0)
project (TinyDbg)


include_directories(ext/libelfin ext/linenoise include)
add_executable(tinydbg src/main.cpp ext/linenoise/linenoise.c)

add_executable(hello tests/hello.cpp)
set_target_properties(hello
                      PROPERTIES COMPILE_FLAGS "-g -O0")

add_executable(stack tests/stack.cpp)
set_target_properties(stack
                      PROPERTIES COMPILE_FLAGS "-g -O0")


add_custom_target(
   libelfin
   COMMAND make
   WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}/ext/libelfin
)
target_link_libraries(tinydbg
                      ${PROJECT_SOURCE_DIR}/ext/libelfin/dwarf/libdwarf++.so
                      ${PROJECT_SOURCE_DIR}/ext/libelfin/elf/libelf++.so)
add_dependencies(tinydbg libelfin)
