##########################################################################
# "THE ANY BEVERAGE-WARE LICENSE" (Revision 42 - based on beer-ware
# license):
# <dev@layer128.net> wrote this file. As long as you retain this notice
# you can do whatever you want with this stuff. If we meet some day, and
# you think this stuff is worth it, you can buy me a be(ve)er(age) in
# return. (I don't like beer much.)
#
# Matthias Kleemann
#
# Modified by Igor Mikolic-Torreira
##########################################################################

cmake_minimum_required( VERSION 2.8 )

### TOOLCHAIN SETUP AREA #################################################
# Set any variables used in the toolchain prior project() call. In that
# case they are already set and used.
##########################################################################

##########################################################################
# tools to beused for programming the AVR
##########################################################################
set( AVR_UPLOADTOOL avrdude )
set( AVR_PROGRAMMER arduino )
set( AVR_UPLOADTOOL_PORT usb )

set( AVR_MCU atmega328p )
set( AVR_MCU_SPEED 160000UL )

### END TOOLCHAIN SETUP AREA #############################################

set( CMAKE_TOOLCHAIN_FILE ../generic-gcc-avr.cmake )

##########################################################################
# name your project
##########################################################################
project( AVR-CPP-EXAMPLE)

##########################################################################
# set build type
##########################################################################
set( CMAKE_BUILD_TYPE Release )

##########################################################################
# include search paths
##########################################################################
include_directories( mycpplib )

#####################################################################
# simple AVR library
#####################################################################
add_avr_library(
   mycpplib
   mycpplib/CLed.cc
   mycpplib/CLed.hh
   )

#####################################################################
# simple AVR executable
#####################################################################
add_avr_executable(
   toggle-led-cpp
   cppapp/main.cc
   )

#####################################################################
# libraries to link to
#####################################################################
target_link_libraries(
   toggle-led-cpp.elf
   mycpplib
   )


