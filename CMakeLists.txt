cmake_minimum_required(VERSION 3.16)
project(python_greenlet LANGUAGES C CXX)

find_package(Python3 COMPONENTS Development REQUIRED)

add_library(_greenlet SHARED src/greenlet/greenlet.cpp)

set_target_properties(_greenlet PROPERTIES
    DEBUG_POSTFIX ""
    OUTPUT_NAME _greenlet
)

target_link_libraries(_greenlet PRIVATE Python3::Python)

target_include_directories(_greenlet INTERFACE
    $<INSTALL_INTERFACE:include>
)

install(FILES src/greenlet/greenlet.h DESTINATION include/)
install(FILES src/greenlet/__init__.py DESTINATION bin/python/greenlet/)
install(TARGETS _greenlet
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)
