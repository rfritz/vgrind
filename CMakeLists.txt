cmake_minimum_required(VERSION 3.20)
project(vgrind LANGUAGES C)

include(CheckSymbolExists)
check_symbol_exists(cgetent "stdlib.h" HAVE_CGETENT)
if(NOT HAVE_CGETENT)
  message(FATAL_ERROR, "vgrind requires BSD cgetent")
endif()

set(APPSHAREPATH ${CMAKE_INSTALL_PREFIX}/share/vgrind)
set(DEFSNAME vgrindefs)

add_executable(vfontedpr vfontedpr.c regexp.c)
target_compile_definitions(vfontedpr PUBLIC
  _PATH_VGRINDEFS="${APPSHAREPATH}/${DEFSNAME}")

# if cap_mkdb is available, generate the defs database
file(COPY ${DEFSNAME}.src DESTINATION .)
file(RENAME ${CMAKE_CURRENT_BINARY_DIR}/${DEFSNAME}.src
  ${CMAKE_CURRENT_BINARY_DIR}/${DEFSNAME})
find_program(CAP_MKDB cap_mkdb)
if(CAP_MKDB)
  add_custom_command(OUTPUT ${DEFSNAME}.db
    COMMAND ${CAP_MKDB} ${DEFSNAME}
    MAIN_DEPENDENCY ${DEFSNAME}
    VERBATIM)
    add_custom_target(defsdb ALL DEPENDS ${DEFSNAME}.db)
endif()

# generate the vgrind csh script
set(VF ${CMAKE_INSTALL_PREFIX}/libexec/vfontedpr)
set(TMDIR ${APPSHAREPATH})
configure_file(vgrind.sh.in vgrind @ONLY)
configure_file(pprint.sh.in pprint @ONLY)

install(TARGETS vfontedpr DESTINATION libexec)
install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/vgrind TYPE BIN)
install(PROGRAMS ${CMAKE_CURRENT_BINARY_DIR}/pprint TYPE BIN)
if(EXISTS ${CMAKE_CURRENT_BINARY_DIR}/vgrindefs.db)
  install(FILES ${CMAKE_CURRENT_BINARY_DIR}/vgrindefs.db
    DESTINATION ${APPSHAREPATH})
else()
  install(FILES ${CMAKE_CURRENT_BINARY_DIR}/vgrindefs
    DESTINATION ${APPSHAREPATH})
endif()
install(FILES vgrind.tmac DESTINATION ${APPSHAREPATH})
install(FILES pprint.1 vgrind.1
  DESTINATION ${CMAKE_INSTALL_PREFIX}/share/man/man1)
install(FILES vgrindefs.5 DESTINATION ${CMAKE_INSTALL_PREFIX}/share/man/man5)
