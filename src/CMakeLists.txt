if(MSVC)
    find_library(WS2_32 ws2_32 REQUIRED)
    find_library(WINMM winmm REQUIRED)
endif()

add_library(snap7)
add_library(snap7::snap7 ALIAS snap7)

target_sources(snap7
    PRIVATE
        core/s7_client.cpp
        core/s7_isotcp.cpp
        core/s7_partner.cpp
        core/s7_peer.cpp
        core/s7_server.cpp
        core/s7_text.cpp
        core/s7_micro_client.cpp

        lib/snap7_libmain.cpp

        sys/snap_msgsock.cpp
        sys/snap_sysutils.cpp
        sys/snap_tcpsrvr.cpp
        sys/snap_threads.cpp
)

target_link_libraries(snap7 PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:${WS2_32} ${WINMM}>
)

target_include_directories(snap7 
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/core
        ${CMAKE_CURRENT_SOURCE_DIR}/lib
        ${CMAKE_CURRENT_SOURCE_DIR}/sys
    INTERFACE
        ${CMAKE_CURRENT_SOURCE_DIR}/../release/Wrappers/c-cpp
)

install(TARGETS snap7
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

if(BUILD_SHARED_LIBS)
    message(STATUS "Building Snap7 as shared library")
else()
    message(STATUS "Building Snap7 as static library")
endif()
