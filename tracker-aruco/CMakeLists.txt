find_package(OpenCV 3.0 QUIET)
if(OpenCV_FOUND)
    set(SDK_ARUCO_LIBPATH "" CACHE FILEPATH "Aruco paper marker tracker static library path")
    if(SDK_ARUCO_LIBPATH)
        otr_module(tracker-aruco)
        target_link_libraries(opentrack-tracker-aruco opentrack-cv ${SDK_ARUCO_LIBPATH} ${OpenCV_LIBS})
        target_include_directories(opentrack-tracker-aruco SYSTEM PUBLIC ${OpenCV_INCLUDE_DIRS})

        # no incremental LTO
        if(MSVC AND MSVC_VERSION GREATER 1910 AND MSVC_VERSION LESS 1950)
            otr_prop(TARGET opentrack-tracker-aruco LINK_FLAGS "/LTCG")
        endif()
    endif()
endif()
