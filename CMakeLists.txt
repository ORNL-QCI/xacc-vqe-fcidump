project(xacc-vqe-fcidump CXX)
cmake_minimum_required(VERSION 3.2)
set(CMAKE_DISABLE_IN_SOURCE_BUILDS ON)
set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_STANDARD_REQUIRED ON)
set(CMAKE_CXX_STANDARD 11)

if(APPLE)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -frtti -fexceptions")
endif()
option(FCIDUMP_BUILD_TESTS "Build test programs" OFF)

if(APPLE)
  set(CMAKE_MACOSX_RPATH 1)
endif()

find_package(XACC REQUIRED)

if (CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set (CMAKE_INSTALL_PREFIX "${XACC_ROOT}" CACHE PATH "default install path" FORCE )
endif()

set(CppMicroServicesConfig_DIR "${XACC_ROOT}/share/cppmicroservices4/cmake")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${XACC_ROOT}/share/xacc")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CppMicroServicesConfig_DIR}")
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules")

include(tests)
include(CppMicroServicesConfig)

set(CMAKE_POSITION_INDEPENDENT_CODE TRUE)

include_directories(${XACC_INCLUDE_DIRS})
include_directories(${CMAKE_SOURCE_DIR}/tpls/CheMPS2/CheMPS2/include) 

link_directories(${XACC_LIBRARY_DIR})
set(ENABLE_TESTS FALSE CACHE BOOL "" FORCE)
add_subdirectory(tpls/CheMPS2)
add_subdirectory(fcidump)

