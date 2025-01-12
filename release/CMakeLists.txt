add_library(snap7_cpp_wrapper STATIC
    Wrappers/c-cpp/snap7.cpp
)
add_library(snap7::cpp_wrapper ALIAS snap7_cpp_wrapper)

target_link_libraries(snap7_cpp_wrapper PUBLIC snap7::snap7)
target_include_directories(snap7_cpp_wrapper INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/Wrappers/c-cpp)
set_target_properties(snap7_cpp_wrapper PROPERTIES
    INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib"
)

install(TARGETS snap7_cpp_wrapper
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)
install(FILES Wrappers/c-cpp/snap7.h DESTINATION include)
