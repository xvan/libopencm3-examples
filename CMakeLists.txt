cmake_minimum_required(VERSION 3.10)

message(STATUS "Current Source Dir: ${CMAKE_CURRENT_SOURCE_DIR}")
set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH};${CMAKE_CURRENT_SOURCE_DIR}/cmake")

set(CMAKE_BUILD_TYPE Debug) 
# Set a default build type if none was specified
set(default_build_type "Debug")

if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to '${default_build_type}' as none was specified.")
  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE
      STRING "Choose the type of build." FORCE)
  # Set the possible values of build type for cmake-gui
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release") 
endif()

message(PROJECT_SOURCE_DIR="${PROJECT_SOURCE_DIR}")

include(toolchain-arm-none-eabi)

set(LINKER_SCRIPT "${CMAKE_CURRENT_SOURCE_DIR}/examples/stm32/f1/stm32-h103/stm32-h103.ld")
set(STARTUP_ASSEMBLY "")
include(stm32fx)

project(libopencm3 C ASM)

add_definitions(-DSTM32F1)
include_directories(libopencm3/include)
link_directories("${CMAKE_CURRENT_SOURCE_DIR}/libopencm3/lib")
add_subdirectory(libopencm3)
add_subdirectory(examples/stm32/f1/stm32-h103)


#add_library(STARTUP OBJECT ${STARTUP_ASSEMBLY})

#add_subdirectory(examples/stm32/f1/stm32-h103/usb_cdcacm)

#FILE(GLOB_RECURSE PROJECT_SRC "Src/*.c")
#set(TARGET ${PROJECT_NAME}.elf)
#add_executable( ${TARGET} ${PROJECT_SRC})
#target_link_libraries(${TARGET} $<TARGET_OBJECTS:STARTUP> $<TARGET_OBJECTS:DRIVERS>)

