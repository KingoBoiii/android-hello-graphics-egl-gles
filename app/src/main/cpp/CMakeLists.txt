cmake_minimum_required(VERSION 3.6.0)

add_library(native_app_glue STATIC ${ANDROID_NDK}/sources/android/native_app_glue/android_native_app_glue.c)
target_include_directories(native_app_glue PUBLIC ${ANDROID_NDK}/sources/android/native_app_glue)

find_library(log-lib log)

set(CMAKE_SHARED_LINKER_FLAGS "${CMAKE_SHARED_LINKER_FLAGS} -u ANativeActivity_onCreate")

add_library(helloandroidgraphics SHARED
    # List C/C++ source files with relative paths to this CMakeLists.txt.
    helloandroidgraphics.cpp)

target_link_libraries(helloandroidgraphics
    # List libraries link to the target library
    native_app_glue
    android
    log
    EGL
    GLESv3)
