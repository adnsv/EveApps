
FILE(GLOB SRCS ../../common/application/*.c Src/*.c)
FILE(GLOB HDRS ../../common/application/*.h Hdr/*.h)
INCLUDE_DIRECTORIES("Hdr")

get_filename_component(ProjectId ${CMAKE_CURRENT_LIST_DIR} NAME)
string(REPLACE " " "_" ProjectId ${ProjectId})
project(${ProjectId} C CXX)

ADD_EXECUTABLE(${ProjectId} ${SRCS} ${HDRS})

IF(EVE_APPS_PLATFORM STREQUAL "RP2040")
  pico_enable_stdio_uart(${ProjectId} 1)
  pico_enable_stdio_usb(${ProjectId} 1) # Enable Virtual COM port
  pico_add_extra_outputs(${ProjectId})
ENDIF()
