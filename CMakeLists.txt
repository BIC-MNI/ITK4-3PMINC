project(ITKMINC)
set(ITKMINC_THIRD_PARTY 1)

option(ITK_USE_SYSTEM_MINC "Use system-installed MINC" OFF)
mark_as_advanced(ITK_USE_SYSTEM_MINC)

if(ITK_USE_SYSTEM_MINC)
  find_package(LIBMINC REQUIRED)
  set(ITKMINC_SYSTEM_INCLUDE_DIRS
    ${LIBMINC_INCLUDE_DIRS}
    )
  set(ITKMINC_LIBRARIES "${LIBMINC_LIBRARIES}")
else()
  set(ITKMINC_INCLUDE_DIRS
    ${ITKMINC_BINARY_DIR}/src
    ${ITKMINC_BINARY_DIR}/src/itkminc2
    ${ITKMINC_SOURCE_DIR}/src
    )
  set(ITKMINC_LIBRARIES itkminc2)
endif()

configure_file(src/itk_minc2.h.in src/itk_minc2.h)

itk_module_impl()

if(NOT ITK_INSTALL_NO_DEVELOPMENT)
  install(FILES ${ITKMINC_BINARY_DIR}/src/itk_minc2.h
    DESTINATION ${ITKMINC_INSTALL_INCLUDE_DIR})
endif(NOT ITK_INSTALL_NO_DEVELOPMENT)
