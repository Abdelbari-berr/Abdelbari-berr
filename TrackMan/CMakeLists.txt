# Nous voulons un cmake "récent" pour utiliser les dernières fonctionnalités
cmake_minimum_required(VERSION 3.0)

# Notre projet est étiqueté TrackMan
#
set(PROJECT_NAME TrackMan)
#
project(${PROJECT_NAME})
#
add_subdirectory(${PROJECT_SOURCE_DIR}/doc)
##
#ADD_SUBDIRECTORY( test )
#ADD_SUBDIRECTORY( test )
#

   
#
#
set(EXECUTABLE_OUTPUT_PATH exe/${CMAKE_BUILD_TYPE})
set(EXECUTABLE_INSTALL_PATH ${CMAKE_SOURCE_DIR}/exe)
set(EXECUTABLE_SOURCE_PATH ${PROJECT_SOURCE_DIR}/exe)
#
set(PROJECT_INC inc ) 
set(PROJECT_LIBS lib) 
set(PROJECT_LLIBS m ) 
set(TYPE_EXE client server console log)
set(TYPE_LIB static shared)

# Trouver un package avec find_package
#
# find_package(GTK2 REQUIRED)
# find_package(PkgConfig)
# pkg_check_modules(GTK2 gtk+-2.0 REQUIRED)
# 
#------------------ OPTIONS ------------------------
#set(PROJECT_OPTIONS -g -Wall -O3 -DUNIX -DLOG_FLAGS)
set(PROJECT_OPTIONS  -Wall -O3 -DUNIX)
#
#------- set list files to compil to object files ------
#
file(
    GLOB_RECURSE
    source_file
    src/*
)

file(
    GLOB_RECURSE
    headers_file
    inc/*
)
#
# message("--------------------------------------------")
#execute_process(COMMAND bash -c "source ${CMAKE_SOURCE_DIR}/env_dev.sh")
#
# --- build project ${PRJECT_NAME} ----
foreach(MODE ${TYPE_LIB} )
    foreach(EXE ${TYPE_EXE} )

        if(${EXE} MATCHES "server")
            add_executable(${PROJECT_NAME}_${EXE}_${MODE} ${source_file} ${headers_file} )
        else()
            add_executable(${PROJECT_NAME}_${EXE}_${MODE} ${source_file} ${headers_file} )
        endif() 
    #
    target_compile_options(${PROJECT_NAME}_${EXE}_${MODE} PUBLIC ${PROJECT_OPTIONS})
    target_include_directories(${PROJECT_NAME}_${EXE}_${MODE} PUBLIC ${PROJECT_INC})
    target_link_libraries(${PROJECT_NAME}_${EXE}_${MODE}   ${PROJECT_LLIBS})
    #

    install (TARGETS ${PROJECT_NAME}_${EXE}_${MODE}  DESTINATION ${EXECUTABLE_SOURCE_PATH})
    install (TARGETS ${PROJECT_NAME}_${EXE}_${MODE}  DESTINATION ${EXECUTABLE_INSTALL_PATH})

    endforeach(${EXE})
endforeach(${MODE})

