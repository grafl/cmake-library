cmake_minimum_required(VERSION 4.0)

project(cmake_library LANGUAGES CXX)

add_library(${PROJECT_NAME} src/library.cpp)
