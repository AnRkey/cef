cmake_minimum_required(VERSION 3.21)

project(libcef_dll_wrapper)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Add include directories
include_directories(include)
include_directories(wrapper)

# Define the wrapper library target
add_library(libcef_dll_wrapper STATIC
    # Wrapper source files
    wrapper/cef_byte_read_handler.cc
    wrapper/cef_closure_task.cc
    wrapper/cef_message_router.cc
    wrapper/cef_message_router_utils.cc
    wrapper/cef_resource_manager.cc
    wrapper/cef_scoped_temp_dir.cc
    wrapper/cef_stream_resource_handler.cc
    wrapper/cef_xml_object.cc
    wrapper/cef_zip_archive.cc
    wrapper/libcef_dll_wrapper2.cc
    wrapper/libcef_dll2.cc
    wrapper/shutdown_checker.cc
    wrapper/transfer_util.cc
)

# Set target properties
set_target_properties(libcef_dll_wrapper PROPERTIES
    PREFIX ""
    OUTPUT_NAME "libcef_dll_wrapper"
)

# Add compile definitions
target_compile_definitions(libcef_dll_wrapper PRIVATE
    -DWRAPPING_CEF_SHARED
    -DUSING_CEF_SHARED
    -DNOMINMAX
    -DWIN32_LEAN_AND_MEAN
)

# Windows specific settings
if(WIN32)
    target_compile_definitions(libcef_dll_wrapper PRIVATE
        -D_WIN32_WINNT=0x0A00
        -DWINVER=0x0A00
    )
endif()

# Set output directory
set_target_properties(libcef_dll_wrapper PROPERTIES
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
) 