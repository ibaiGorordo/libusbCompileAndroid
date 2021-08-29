# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.10.2)

# Declares and names the project.

project("libusbcompileandroid")

######         libusb         ######
set(LIBUSB_DIR ${CMAKE_SOURCE_DIR}/libusb)
set(LIBUSB_SOURCES ${LIBUSB_DIR}/libusb/core.c
        ${LIBUSB_DIR}/libusb/descriptor.c
        ${LIBUSB_DIR}/libusb/hotplug.c
        ${LIBUSB_DIR}/libusb/io.c
        ${LIBUSB_DIR}/libusb/sync.c
        ${LIBUSB_DIR}/libusb/strerror.c
        ${LIBUSB_DIR}/libusb/os/linux_usbfs.c
        ${LIBUSB_DIR}/libusb/os/events_posix.c
        ${LIBUSB_DIR}/libusb/os/threads_posix.c
        ${LIBUSB_DIR}/libusb/os/linux_netlink.c
        )

include_directories(${LIBUSB_DIR}
        ${LIBUSB_DIR}/android
        ${LIBUSB_DIR}/libusb
        ${LIBUSB_DIR}/libusb/os
        )

add_library( # Sets the name of the library.
        usb-1.0

        # Sets the library as a shared library.
        SHARED

        # Provides a relative path to your source file(s).
        ${LIBUSB_SOURCES})


find_library( # Sets the name of the path variable.
        log-lib

        # Specifies the name of the NDK library that
        # you want CMake to locate.
        log)

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        usb-1.0

        # Links the target library to the log library
        # included in the NDK.
        ${log-lib})