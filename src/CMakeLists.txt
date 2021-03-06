# This Source Code Form is subject to the terms of the Mozilla Public
# License, v. 2.0. If a copy of the MPL was not distributed with this
# file, You can obtain one at http://mozilla.org/MPL/2.0/.

set(HINDSIGHT_SRC
hindsight.c
hs_analysis_plugins.c
hs_checkpoint_reader.c
hs_checkpoint_writer.c
hs_config.c
hs_input.c
hs_input_plugins.c
hs_logger.c
hs_output.c
hs_output_plugins.c
hs_util.c
)

set(HINDSIGHT_LIBS
${LUASANDBOX_LIBRARIES}
${UNIX_LIBRARIES})

set(CMAKE_SKIP_BUILD_RPATH FALSE CACHE STRING "" FORCE)
set(CMAKE_BUILD_WITH_INSTALL_RPATH FALSE CACHE STRING "" FORCE)
set(CPACK_RPM_PACKAGE_LICENSE "MPLv2.0")
set(CPACK_STRIP_FILES TRUE)

add_executable(hindsight ${HINDSIGHT_SRC})
set(HINDSIGHT_LIBS
${LUASANDBOX_LIBRARIES}
${UNIX_LIBRARIES})

target_link_libraries(hindsight ${HINDSIGHT_LIBS})

add_executable(hindsight_cli ${HINDSIGHT_SRC})

target_compile_definitions(hindsight_cli PUBLIC "-DHINDSIGHT_CLI")
target_link_libraries(hindsight_cli ${HINDSIGHT_LIBS})

install(TARGETS hindsight DESTINATION bin)
install(TARGETS hindsight_cli DESTINATION bin)

add_subdirectory(test)
