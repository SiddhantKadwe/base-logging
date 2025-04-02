cmake_minimum_required(VERSION 3.10)
project(base-logging VERSION 0.2)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

# Define sources and headers
set(BASE_LOGGING_SOURCES
    src/logging/logging_printf_style.cpp
)
set(BASE_LOGGING_CORE_HEADERS
    src/Logging.hpp
    src/Singleton.hpp
)
set(BASE_LOGGING_STYLE_HEADERS
    src/logging/logging_printf_style.h
    src/logging/logging_iostream_style.h
)

# Create the base_logging library
add_library(base-logging 
            ${BASE_LOGGING_SOURCES} 
            ${BASE_LOGGING_CORE_HEADERS} 
            ${BASE_LOGGING_STYLE_HEADERS}
            )
            
target_include_directories(base-logging PUBLIC 
                           ${CMAKE_CURRENT_SOURCE_DIR}/src)

# Optionally, generate a pkg-config file if needed
configure_file(base-logging.pc.in ${CMAKE_BINARY_DIR}/base-logging.pc @ONLY)
install(FILES ${CMAKE_BINARY_DIR}/base-logging.pc DESTINATION lib/pkgconfig)

# Install library and headers
install(TARGETS base-logging
    EXPORT base-logging-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)
install(FILES ${BASE_LOGGING_CORE_HEADERS}
    DESTINATION include/base-logging/
)
install(FILES ${BASE_LOGGING_STYLE_HEADERS}
    DESTINATION include/base-logging/logging/
)
