# Nous voulons un cmake "récent" pour utiliser les dernières fonctionnalités
cmake_minimum_required(VERSION 3.0)

set(PROJECT_NAME Test_Lib_TrackCalculatorAgent LANGUAGES CXX)

find_package(Catch2 CONFIG REQUIRED)

include(CTest)


message( STATUS "Test included" )

# Add catch as an interface library
set(CATCH_INCLUDE_DIR  /usr/local/include/catch2/catch_test_macros.hpp  /usr/local/include/catch2  /usr/local/include/catch2/catch_user_config.hpp)
target_include_directories(Catch INTERFACE ${CATCH_INCLUDE_DIR})
add_library(Catch INTERFACE)
include (Catch)


add_subdirectory(src)



# Add test executable
add_executable (tests-Lib_TrackCalculatorAgent
                src/testmain.cpp 
                src/testA.cpp
                src/testB.cpp)
                
#target_link_libraries(tests Catch CommonSourceCode)
target_link_libraries(tests-Lib_TrackCalculatorAgent PRIVATE ../ Catch2::Catch2)

add_test(NAME tests-Lib_TrackCalculatorAgent COMMAND LibTests)
catch_discover_tests(MyLibTests)