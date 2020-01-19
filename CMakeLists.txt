cmake_minimum_required(VERSION 3.0)

include(tacklelib/Project)

project("sgp4")

set(PROJECT_LIB_NAME sgp4)

# enable c++ standard usage for all targets, basically to avoid the default `--std=gnu++11` parameter for the GCC compiler
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

tkl_check_var(OPTIONAL PATH QD_ROOT)
tkl_check_var(OPTIONAL . ENABLE_QD_INTEGRATION)
tkl_check_var(OPTIONAL . ENABLE_QD_QD_INTEGRATION)
tkl_check_var(OPTIONAL . ENABLE_QD_DD_INTEGRATION)


# Workaround for the issue: https://stackoverflow.com/questions/51272106/cmake-add-subdirectory-twice-as-a-shared-project
#
# The error:
#
#   CMake Error at _3dparty/sat/sgp4/CMakeLists.txt:XX (target_link_libraries):
#     Attempt to add link library "qd" to target "sgp4" which is not built in
#     this directory.
#
file(GLOB_RECURSE all_headers ${CMAKE_CURRENT_LIST_DIR}/libsgp4/*.h*)
file(GLOB_RECURSE all_sources ${CMAKE_CURRENT_LIST_DIR}/libsgp4/*.c*)

add_library(${PROJECT_LIB_NAME} STATIC ${all_headers};${all_sources})
#add_library(${PROJECT_LIB_NAME}s SHARED ${all_headers};${all_sources})

tkl_initialize_library_target_defaults(${PROJECT_LIB_NAME} "32bit")
#tkl_initialize_library_target_defaults(${PROJECT_LIB_NAME}s "32bit")

#add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/libsgp4) # otherwise the error would appear

tkl_source_groups_from_dir_list("Header Files" FILES ${CMAKE_CURRENT_LIST_DIR} *.h*)
tkl_source_groups_from_dir_list("Source Files" FILES ${CMAKE_CURRENT_LIST_DIR} *.c*)

#target_include_directories(${PROJECT_LIB_NAME}
#  PUBLIC
#    ${CMAKE_CURRENT_LIST_DIR}/core
#)

foreach(target ${PROJECT_LIB_NAME})#;${PROJECT_LIB_NAME}s)
  if(WIN32)
    tkl_add_target_compile_definitions(${target} *
      PUBLIC
        _X86_   # basically defined by MinGW, so define explicitly to compile in MSVC
    )
  endif()

  if(GCC)
    tkl_add_target_compile_properties(${target} *
      # from library authors
      -Wall -Wextra -Wshadow -Wshadow -Wnon-virtual-dtor -pedantic -Wno-long-long
      -Wcast-align -Wsign-conversion
    )
  endif()
endforeach()

# integration with QD

tkl_add_target_subdirectory(QD_ROOT qd ${CMAKE_BUILD_ROOT}/_3dparty/math/qd)

add_dependencies(${PROJECT_LIB_NAME} qd)

target_link_libraries(${PROJECT_LIB_NAME} # the workaround for the error from here
  PUBLIC
    qd
)

