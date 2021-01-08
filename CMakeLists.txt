cmake_minimum_required(VERSION 3.0.0)
project(deutex VERSION 2.0)
set(CMAKE_CXX_CLANG_TIDY
    clang-tidy;
    -header-filers=.;
    -checks=*)

add_subdirectory("src")
