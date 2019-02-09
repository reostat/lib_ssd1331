cmake_minimum_required(VERSION 3.5)
project(ssd1331 LANGUAGES C VERSION 0.0.1)

include(GNUInstallDirs)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Werror=format-security \
    -Werror=implicit-function-declaration -Werror=return-type")

add_library(ssd1331 STATIC src/ftdi_util.c src/ssd_displ.c src/ssd_displ_graph.c)

target_include_directories(ssd1331 PUBLIC include)
target_link_libraries(ssd1331 ftdi)

set_target_properties(ssd1331 PROPERTIES
    VERSION ${PROJECT_VERSION}
    PUBLIC_HEADER include/ftdi_util.h include/ssd_displ.h include/ssd_displ_graph.h)

install(TARGETS ssd1331
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
