cmake_minimum_required(VERSION 3.17)
project(QtDocumentGenerator CXX)

set(CMAKE_CXX_STANDARD 17)

if (DEFINED QT_DIR)
    message(STATUS "QT CMAKE DIR....${QT_DIR}")
else()
    message(FATAL_ERROR "QT_DIR variable is unset. \n  ")
endif()

set(CMAKE_PREFIX_PATH ${QT_DIR})

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(SOURCE_FILES TDB.cpp)
set(PRIVATE_HEADERS TDB_p.h)
set(PUBLIC_HEADERS include/QtDocumentGenerator/qtdocumentgenerator_global.h)

add_definitions(-DQTDOCUMENTGENERATOR_LIB)
add_library(QtDocumentGenerator)

find_package(Qt5 COMPONENTS Core REQUIRED)

target_sources(QtDocumentGenerator PRIVATE ${SOURCE_FILES} ${PRIVATE_HEADERS}) 
target_sources(QtDocumentGenerator PUBLIC ${PUBLIC_HEADERS})

target_include_directories(QtDocumentGenerator  PUBLIC ${CMAKE_CURRENT_BINARY_DIR}/include)
target_include_directories(QtDocumentGenerator PRIVATE ${CMAKE_CURRENT_BINARY_DIR}/src)

target_link_libraries(QtDocumentGenerator Qt5::Core )
