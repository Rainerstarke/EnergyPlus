
INCLUDE_DIRECTORIES( "${CMAKE_SOURCE_DIR}/third_party/Expat/lib")
INCLUDE_DIRECTORIES( "${CMAKE_SOURCE_DIR}/third_party/")

SET(SRC 
  main.h
  main.c
  fmiFunctions.h
  fmiModelTypes.h
  fmiPlatformTypes.h
  fmumini.c
  fmumini.h
  stack.c
  stack.h
  util.c
  util.h
  xml_parser_cosim.c
  xml_parser_cosim.h
  eplusModelFunctions.h
  fmiModelFunctions.h
  fmiModelTypes.h
)

ADD_LIBRARY( epfmiimport SHARED ${SRC} )

IF( MSVC )
  ADD_DEFINITIONS( "/w" )
ELSE()
  ADD_DEFINITIONS( "-w" )
ENDIF()

TARGET_LINK_LIBRARIES( epfmiimport epexpat miniziplib )

INSTALL( TARGETS epfmiimport 
  RUNTIME DESTINATION ./ 
  LIBRARY DESTINATION ./ 
)

if( UNIX )
set_target_properties(
  epfmiimport
  PROPERTIES
  INSTALL_NAME_DIR "@executable_path"
)
endif()

