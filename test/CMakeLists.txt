file(GLOB TEST_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/*.f90")

foreach(test_src IN LISTS TEST_SOURCES)
  get_filename_component(test_name "${test_src}" NAME_WE)

  add_executable("${test_name}" "${test_src}")
  target_link_libraries("${test_name}" PRIVATE interpolation2d3d)

  # Ensure test exe can find the module files from the library build
  # (usually already handled by target_include_directories on the library,
  # but keeping it explicit is harmless).
  target_include_directories("${test_name}" PRIVATE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/../mod>
  )

  add_test(NAME "${test_name}" COMMAND "${test_name}")
endforeach()