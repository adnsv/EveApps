IF(EVE_APPS_PLATFORM STREQUAL "RP2040")
    get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
    message( WARNING "${ProjectId} Not support RP2040" )
    return()
ENDIF()
    
FILE(GLOB SRCS ../../common/application/*.c Src/*.c libs/AviPlayer/*.c libs/Heap/*.c libs/MediaPlayer/*.c)
FILE(GLOB HDRS ../../common/application/*.h Hdr/*.h)

INCLUDE_DIRECTORIES("Hdr")
INCLUDE_DIRECTORIES("libs/AviPlayer")
INCLUDE_DIRECTORIES("libs/Heap")
INCLUDE_DIRECTORIES("libs/MediaPlayer")

get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId})
project(${ProjectId} C CXX)

ADD_EXECUTABLE(${ProjectId} ${SRCS} ${HDRS})

IF(EVE_APPS_PLATFORM STREQUAL "RP2040")
  pico_enable_stdio_uart(${ProjectId} 1)
  pico_enable_stdio_usb(${ProjectId} 1) # Enable Virtual COM port
  pico_add_extra_outputs(${ProjectId})
ENDIF()
