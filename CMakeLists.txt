project(kcm_ufw)
set(PROJECT_VERSION "0.6.2")

cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)

set(QT_MIN_VERSION "5.2.0")
set(KF5_MIN_VERSION "5.1.0")


# Silence a warning
cmake_policy(SET CMP0037 OLD)

find_package(ECM 1.1.0 REQUIRED NO_MODULE)

set(CMAKE_MODULE_PATH ${ECM_MODULE_PATH} ${ECM_KDE_MODULE_DIR})
set(CMAKE_AUTOMOC ON)
set(CMAKE_INCLUDE_CURRENT_DIR ON)

find_package(Qt5 ${QT_MIN_VERSION} CONFIG REQUIRED COMPONENTS
             Widgets
             DBus
             Network)
             
find_package(KF5 ${KF5_MIN_VERSION} REQUIRED COMPONENTS
             Auth
             ConfigWidgets
             CoreAddons
             Crash
             I18n
             KIO
             #Network
             WidgetsAddons)
             
include_directories(${Qt5Network_INCLUDE_DIRS})

include(KDEInstallDirs)
include(KDECompilerSettings)
include(KDECMakeSettings)
include(FeatureSummary)
include(CheckIncludeFiles)

find_package(PkgConfig REQUIRED)
#pkg_check_modules(UFW "ufw" REQUIRED)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fexceptions")
# Adding local CMake modules
set (
   CMAKE_MODULE_PATH
   ${CMAKE_CURRENT_SOURCE_DIR}/cmake/modules
   ${CMAKE_MODULE_PATH}
)

configure_file(config.h.cmake ${CMAKE_BINARY_DIR}/config.h)

add_definitions(-DTRANSLATION_DOMAIN=\"kcm-ufw\")

add_subdirectory(helper)
add_subdirectory(kcm)

#add_subdirectory(doc)

ki18n_install(po)

#kde4_install_icons( ${ICON_INSTALL_DIR} )

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)
