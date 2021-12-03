## Authors: first_name1 last_name1, first_name2 last_name2
########################################################################################################################

cmake_minimum_required(VERSION 3.16.3)

project("Programming Project: Galaxy-Crash"
        VERSION 1.0
        LANGUAGES CXX)


########################################################################################################################
##                                                   create library                                                   ##
########################################################################################################################
## TODO: all source files (*.cpp) must be added here (*.cpp)
set(LIBRARY_SOURCES src/nbody/dummy.cpp)

# create library
set(LIBRARY_NAME n-body)
add_library(${LIBRARY_NAME} STATIC ${LIBRARY_SOURCES})


########################################################################################################################
##                                                 set compiler flags                                                 ##
########################################################################################################################
# set C++17 as standard
target_compile_features(${LIBRARY_NAME} PUBLIC cxx_std_17)
# set include as include-directory
target_include_directories(${LIBRARY_NAME} PUBLIC include)
# add warning flags based on the used C++-compiler
target_compile_options(${LIBRARY_NAME} PUBLIC
        $<$<CXX_COMPILER_ID:GNU,Clang>:-Wall -Wextra -Wpedantic -Werror>
        $<$<CXX_COMPILER_ID:MSVC>:/W4 /WX>
)
# add math definition
target_compile_definitions(${LIBRARY_NAME} PUBLIC _USE_MATH_DEFINES)


# create executable
add_executable(simulate src/main.cpp)

# link library against executable
target_link_libraries(simulate PRIVATE ${LIBRARY_NAME})
