set(SOURCES
        main.cpp
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(asteroid ${SOURCES})

include_directories(${SFML_INCLUDE_DIR})
target_link_libraries(asteroid ${SFML_LIBRARIES})
