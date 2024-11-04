set(CMAKE_CXX_STANDARD 11)
cmake_minimum_required(VERSION 3.16)

project(cpp_monkey)

add_library(lib_monkey "")
target_sources(lib_monkey
    PRIVATE
    "header/ast.h"
    "header/environment.h"
    "header/evaluator.h"
    "header/lexer.h"
    "header/object.h"
    "header/parser.h"
    "header/token.h"

    "src/ast.cpp"
    "src/evaluator.cpp"
    "src/lexer.cpp"
    "src/object.cpp"
    "src/parser.cpp"
    "src/token.cpp"
)
include_directories(AFTER ${CMAKE_SOURCE_DIR}/header)

add_executable(monkey_test)
target_sources(monkey_test
    PRIVATE
    "tests/ast_test.cpp"
)
add_subdirectory("third_party/googletest")
target_link_libraries(monkey_test PRIVATE lib_monkey gtest gtest_main)

add_executable(monkey)
target_sources(monkey
    PRIVATE
    "main.cpp"
)
target_link_libraries(monkey PRIVATE lib_monkey)

