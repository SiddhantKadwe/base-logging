cmake_minimum_required(VERSION 3.10)
project(base_logging)

# Define sources and headers
set(BASE_LOGGING_SOURCES
    src/logging/logging_printf_style.cpp
)
set(BASE_LOGGING_HEADERS
    src/logging/Logging.hpp
    src/logging/logging_printf_style.h
    src/logging/logging_iostream_style.h
    src/logging/Singleton.hpp
)

# Create the base_logging library
add_library(base_logging ${BASE_LOGGING_SOURCES} ${BASE_LOGGING_HEADERS})
target_include_directories(base_logging PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Optionally, generate a pkg-config file if needed
configure_file(base_logging.pc.in ${CMAKE_BINARY_DIR}/base_logging.pc @ONLY)
install(FILES ${CMAKE_BINARY_DIR}/base_logging.pc DESTINATION lib/pkgconfig)

# Install library and headers
install(TARGETS base_logging
    EXPORT base_logging-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)
install(FILES ${BASE_LOGGING_HEADERS}
    DESTINATION include/base_logging/logging
)