cmake_minimum_required(VERSION 3.10)

# Indicating project name
project(base)

# Indicating the path of my cpp files, if I have headers I need to specify here.
add_executable(base
    src/main.cpp
)

# If it fails to find png, will enter here
if(NOT PNG AND WIN32 AND NOT MSVC)
    set(PNG_LIBRARY "C:/Program Files (x86)/libpng")
    set(PNG_PNG_INCLUDE_DIR "C:/Program Files (x86)/libpng/include") 
endif()

# Looking for the libraries
find_package(SDL3 REQUIRED)
find_package(SDL3_image REQUIRED)

# Does not find the directories.
# Print debug information
message(STATUS "SDL3_INCLUDE_DIRS: ${SDL3_INCLUDE_DIRS}")
message(STATUS "SDL3_IMAGE_INCLUDE_DIRS: ${SDL3_IMAGE_INCLUDE_DIRS}")
message(STATUS "SDL3_LIBRARIES: ${SDL3_LIBRARIES}")

# Setting include directories
target_include_directories(base
    PUBLIC ${SDL3_INCLUDE_DIRS}
    PUBLIC ${SDL3_IMAGE_INCLUDE_DIRS}
)

# Linking libraries
if(WIN32 AND NOT MSVC)
    target_link_libraries(base PUBLIC ${SDL3_LIBRARIES} SDL3_image::SDL3_image mingw32)
else()
    target_link_libraries(base PUBLIC ${SDL3_LIBRARIES} SDL3_image::SDL3_image)
endif()
