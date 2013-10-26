cmake_minimum_required(VERSION 2.8)

PROJECT(serializableFSM)

IF(WIN32)
                add_definitions(-D_CRT_SECURE_NO_WARNINGS -DWIN_MVC)
ENDIF(WIN32)

IF(CMAKE_COMPILER_IS_GNUCXX)
   add_definitions(-Wall -Wno-unknown-pragmas ) #removing pragma once...
ENDIF(CMAKE_COMPILER_IS_GNUCXX)

#################################################
# BOOST
################################################
SET(BOOST_ROOT "$ENV{BOOST}")
SET(Boost_USE_STATIC_LIBS ON)
SET(Boost_USE_MULTITHREADED ON)
UNSET(Boost_INCLUDE_DIR CACHE)
UNSET(Boost_LIBRARY_DIRS CACHE)
FIND_PACKAGE(Boost REQUIRED COMPONENTS serialization)
INCLUDE_DIRECTORIES(AFTER SYSTEM  ${Boost_INCLUDE_DIR})


###########################################################
# SENDER
###########################################################
SET(SENDER_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include)
SET(SENDER_SRC_DIR  ${CMAKE_CURRENT_SOURCE_DIR}/src)
FILE(GLOB SENDER_SRC ${SENDER_SRC_DIR}/*.cpp)
FILE(GLOB SENDER_HDR ${SENDER_INCLUDE_DIR}/*.h)
INCLUDE_DIRECTORIES(AFTER SYSTEM  ${SENDER_INCLUDE_DIR})
SET(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/)

ADD_EXECUTABLE(${PROJECT_NAME} ${SENDER_SRC} )
TARGET_LINK_LIBRARIES(${PROJECT_NAME}  ${Boost_LIBRARIES})
