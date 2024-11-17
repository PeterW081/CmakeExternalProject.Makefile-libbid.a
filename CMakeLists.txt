set(VAR_cmake_version "3.12")
set(VAR_project_name "ExternalProject::bid")  ## https://www.intel.com/content/www/us/en/developer/articles/tool/intel-decimal-floating-point-math-library.html

###
cmake_minimum_required(VERSION "${VAR_cmake_version}")
project("${VAR_project_name}")

###
set(VAR_project_name-01ExternalProjectBuildx "${VAR_project_name}")
set(VAR_project_name-02ExternalProjectImport "${VAR_project_name}-IMPORT")
string(REGEX REPLACE "^ExternalProject::" "ExternalProject-" "VAR_project_name-01ExternalProjectBuildx" "${VAR_project_name-01ExternalProjectBuildx}")
string(REGEX REPLACE "^ExternalProject::" "ExternalProject-" "VAR_project_name-02ExternalProjectImport" "${VAR_project_name-02ExternalProjectImport}")

###
add_library(
  "${VAR_project_name-02ExternalProjectImport}" INTERFACE
)
add_library(
  "${VAR_project_name}" ALIAS "${VAR_project_name-02ExternalProjectImport}"
)

###
include(ExternalProject)
ExternalProject_Add(
  "${VAR_project_name-01ExternalProjectBuildx}"
  PREFIX "${CMAKE_BINARY_DIR}/_deps_external_project/"
  BUILD_IN_SOURCE 1
  CONFIGURE_COMMAND ""
  INSTALL_COMMAND ""
  #
  URL "file://${PROJECT_SOURCE_DIR}/IntelRDFPMathLib20U2.tar.gz"                                ##
  URL_MD5 "DF7CDBF4B02F4A46AA38A64F7DFF69E0"                                                    ##
  SOURCE_SUBDIR "LIBRARY/"                                                                      ##
  BUILD_COMMAND make CC=gcc CALL_BY_REF=0 GLOBAL_RND=0 GLOBAL_FLAGS=0 UNCHANGED_BINARY_FLAGS=0  ##
  INSTALL_COMMAND ""                                                                            ##
)
add_dependencies(
  "${VAR_project_name-02ExternalProjectImport}"
  "${VAR_project_name-01ExternalProjectBuildx}"
)
##X
ExternalProject_Get_Property("${VAR_project_name-01ExternalProjectBuildx}" SOURCE_DIR)
ExternalProject_Get_Property("${VAR_project_name-01ExternalProjectBuildx}" SOURCE_SUBDIR)
target_include_directories(
  "${VAR_project_name-02ExternalProjectImport}" INTERFACE
  "${SOURCE_DIR}/${SOURCE_SUBDIR}/src/"                                                         ##
)
target_link_libraries(
  "${VAR_project_name-02ExternalProjectImport}" INTERFACE
  "${SOURCE_DIR}/${SOURCE_SUBDIR}/libbid.a"                                                     ##
)
unset(SOURCE_DIR)
unset(SOURCE_SUBDIR)

