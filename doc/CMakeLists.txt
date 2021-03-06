# Copyright: (C) 2009 RobotCub Consortium
# Authors: Paul Fitzpatrick
# CopyPolicy: Released under the terms of the LGPLv2.1 or later, see LGPL.TXT

find_package(Doxygen)

if(DOXYGEN_FOUND)
    set(DOX_GENERATE_HTML YES)
    set(DOX_GENERATE_XML NO)
    option(CODYCO_DOXYGEN_XML "Generate doxygen XML output, for use by SWIG" NO)
    mark_as_advanced(CODYCO_DOXYGEN_XML)
    if(CODYCO_DOXYGEN_XML)
        set(DOX_GENERATE_XML YES)
    endif()
    # CoDyCo documentation is always verbose now.  It used to be
    # partially stripped of stuff less interesting to end-users.
    set(DOX_EXTRA_DIR src conf doc/spec)
    set(DOX_PATTERNS "*.h *.dox *.cpp")
    set(DOX_GENERATE_MAN NO)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
                   ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)
    add_custom_target(dox COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile)

    set(DOX_GENERATE_HTML NO)
    set(DOX_GENERATE_MAN YES)
    set(DOX_GENERATE_XML NO)
    set(DOX_PATTERNS "cmd_*.dox")
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
                   ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile.man)
    add_custom_target(man COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile.man)
endif()
