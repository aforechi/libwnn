FIND_PACKAGE(SWIG REQUIRED)
INCLUDE(${SWIG_USE_FILE})
FIND_PACKAGE(PythonLibs REQUIRED)

SET_SOURCE_FILES_PROPERTIES(libwnn.i PROPERTIES CPLUSPLUS ON)
INCLUDE_DIRECTORIES(${PYTHON_INCLUDE_PATH})

SET(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/python)

SWIG_ADD_MODULE(libwnn python libwnn.i)
SWIG_LINK_LIBRARIES(libwnn wnn ${PYTHON_LIBRARIES})

execute_process(COMMAND python -c "from distutils.sysconfig import get_python_lib; print(get_python_lib())" OUTPUT_VARIABLE PYTHON_SITE_PACKAGES OUTPUT_STRIP_TRAILING_WHITESPACE)
install(FILES ${CMAKE_BINARY_DIR}/python/_libwnn.so ${CMAKE_BINARY_DIR}/python/libwnn.py DESTINATION ${PYTHON_SITE_PACKAGES})
