##########################################################################
# "THE ANY BEVERAGE-WARE LICENSE" (Revision 42 - based on beer-ware
# license):
# <dev@layer128.net> wrote this file. As long as you retain this notice
# you can do whatever you want with this stuff. If we meet some day, and
# you think this stuff is worth it, you can buy me a be(ve)er(age) in
# return. (I don't like beer much.)
#
# Matthias Kleemann
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

##########################################################################
# AVR and fuses needs to be set
##########################################################################
set( AVR_MCU atmega2560 )
set( AVR_MCU_SPEED "16000000UL" )


### END TOOLCHAIN SETUP AREA #############################################

# Intentionally left blank, due to a different approach of using the
# toolchain file via -DCMAKE_TOOLCHAIN_FILE=path/to/generic-gcc-avr.cmake
# at the cmake command line call
#
set( CMAKE_TOOLCHAIN_FILE ../generic-gcc-avr.cmake )

##########################################################################
# name your project
##########################################################################
project( AVR-EXAMPLE )

##########################################################################
# set build type
##########################################################################
set( CMAKE_BUILD_TYPE Release )



include_directories( mylib )

##########################################################################
# building library and application in their subdirectories
##########################################################################
add_avr_executable( TestIt app/main.c mylib/mylib.c )

avr_target_link_libraries( TestIt m c )



##########################################################################
# testing functions w/o source files - gets FATAL_ERROR
##########################################################################
# add_avr_executable(test_breaks_generation)
# add_avr_library(mytestlib_breaks_generation)



