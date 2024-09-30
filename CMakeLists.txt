cmake_minimum_required(VERSION 3.29)
project(example LANGUAGES NONE)

find_program(EXAMPLE NAMES example HINTS "${CMAKE_SOURCE_DIR}" REQUIRED)

set(STAMP_FILE "${CMAKE_BINARY_DIR}/example.stamp")
add_custom_command(
  OUTPUT "${STAMP_FILE}"
  COMMAND "${CMAKE_COMMAND}" -E echo "before"
  COMMAND "${EXAMPLE}"
  # Nothing below here is executed
  COMMAND "${CMAKE_COMMAND}" -E echo "after"
  COMMAND "${CMAKE_COMMAND}" -E touch "${STAMP_FILE}"
)

add_custom_target(test ALL DEPENDS "${STAMP_FILE}")
