# For more information about using CMake with Android Studio, read the
# documentation: https://d.android.com/studio/projects/add-native-code.html

# Sets the minimum version of CMake required to build the native library.

cmake_minimum_required(VERSION 3.4.1)

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.

add_library( # Sets the name of the library.
             mirrorai

             # Sets the library as a shared library.
             SHARED

             # Provides a relative path to your source file(s).
             src/main/cpp/mirrorai.cpp)

add_library(
     bgfx
     STATIC
     IMPORTED
)
set_target_properties(bgfx PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libbgfxRelease.a)

add_library(
     bimg_decode
     STATIC
     IMPORTED
)
set_target_properties(bimg_decode PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libbimg_decodeRelease.a)

add_library(
     bimg
     STATIC
     IMPORTED
)
set_target_properties(bimg PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libbimgRelease.a)

add_library(
     bx
     STATIC
     IMPORTED
)
set_target_properties(bx PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/src/main/jniLibs/${ANDROID_ABI}/libbxRelease.a)

# Searches for a specified prebuilt library and stores the path as a
# variable. Because CMake includes system libraries in the search path by
# default, you only need to specify the name of the public NDK library
# you want to add. CMake verifies that the library exists before
# completing its build.

find_library( # Sets the name of the path variable.
              log-lib

              jnigraphics

              # Specifies the name of the NDK library that
              # you want CMake to locate.
              log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

include_directories( src/main/cpp/bgfx/include src/main/cpp/bimg/include src/main/cpp/bx/include )

target_link_libraries( # Specifies the target library.
                       mirrorai
                       jnigraphics
                       bgfx
                       bimg_decode
                       bimg
                       bx
                       EGL
                       GLESv2
                       log
                       android
                       # Links the target library to the log library
                       # included in the NDK.
                       ${log-lib} )