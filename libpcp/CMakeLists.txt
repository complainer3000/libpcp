# Collect source and include files
file(GLOB_RECURSE LIBPCP_SRC_FILES "src/*.c")
file(GLOB_RECURSE LIBPCP_INC_FILES "include/*.h")

# If on Windows, add Windows-specific files and directories
if (WIN32)
    file(GLOB_RECURSE WIN_SRC_FILES "src/windows/*.c")
    file(GLOB_RECURSE WIN_INC_FILES "include/windows/*.h")
    list(APPEND LIBPCP_SRC_FILES ${WIN_SRC_FILES})
    list(APPEND LIBPCP_INC_FILES ${WIN_INC_FILES})
    include_directories(include/windows win_utils)
endif()

# Include main source and include directories
include_directories(src include)

# Create the library
add_library(${LIB_LIBPCP} STATIC ${LIBPCP_SRC_FILES} ${LIBPCP_INC_FILES})

# Link libraries if on Windows
if (WIN32)
    target_link_libraries(${LIB_LIBPCP})
endif()
