project(kcm_ufw)
cmake_minimum_required(VERSION 2.6.0)

set(CPACK_PACKAGE_DESCRIPTION_FILE "${CMAKE_CURRENT_SOURCE_DIR}/README")
set(CPACK_GENERATOR "DEB;RPM;TGZ")
set(DEBIAN_PACKAGE_DESCRIPTION "KDE4 GUI for uncomplicated-firewall")
set(DEBIAN_PACKAGE_SECTION "kde4")
set(CPACK_SOURCE_GENERATOR "TBZ2")
set(CPACK_PACKAGE_VERSION_MAJOR "0")
set(CPACK_PACKAGE_VERSION_MINOR "5")
set(CPACK_PACKAGE_VERSION_PATCH "0")
set(CPACK_PACKAGE_CONTACT "Craig Drummond <craig.p.drummond@gmail.com>")
set(KCM_UFW_VERSION "${CPACK_PACKAGE_VERSION_MAJOR}.${CPACK_PACKAGE_VERSION_MINOR}")
set(KCM_UFW_VERSION_FULL "${KCM_UFW_VERSION}.${CPACK_PACKAGE_VERSION_PATCH}")
set(CPACK_SOURCE_PACKAGE_FILE_NAME "${CMAKE_PROJECT_NAME}-${KCM_UFW_VERSION_FULL}")
set(CPACK_PACKAGE_FILE_NAME "${CMAKE_PROJECT_NAME}-${KCM_UFW_VERSION_FULL}")
include(CPack)

find_package(KDE4 REQUIRED)
configure_file(config.h.cmake ${CMAKE_BINARY_DIR}/config.h)

add_subdirectory( helper )
add_subdirectory( kcm )

if (NOT UFW_TRANSLATIONS)
    set(UFW_TRANSLATIONS "all")
endif (NOT UFW_TRANSLATIONS)

foreach(trans ${UFW_TRANSLATIONS})
    if (trans STREQUAL "all")
        set(UFW_EN_TRANSLATION 1)
        set(UFW_ES_TRANSLATION 1)
        set(UFW_FR_TRANSLATION 1)
        set(UFW_LT_TRANSLATION 1)
    elseif (trans STREQUAL "en")
        set(UFW_EN_TRANSLATION 1)
    elseif (trans STREQUAL "es")
        set(UFW_ES_TRANSLATION 1)
    elseif (trans STREQUAL "fr")
        set(UFW_FR_TRANSLATION 1)
    elseif (trans STREQUAL "lt")
        set(UFW_LT_TRANSLATION 1)
    endif (trans STREQUAL "all")
endforeach(trans ${UFW_TRANSLATIONS})

add_subdirectory(doc)

#kde4_install_icons( ${ICON_INSTALL_DIR} )