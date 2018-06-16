## Prerequisite

**NOTE: SFML 2.5 handles CMake on a different way than 2.4. This tutorial was made on Xubuntu 17.10 where the repository contains the 2.4 version, so the project CMake files made according to that version. In the next section I will provide description to configure booth of them.**

### Install SFML to your computer
https://www.sfml-dev.org/tutorials/2.5/start-linux.php

### SFML 2.4 section

If you successfully compile the link's main.cpp with the g++ command your installation is good. On the other hand, this project uses CMake for the build so you may have to check the following file.

```
whereis SFML
```
The command will show where are the SFML related files.

Output:

```
SFML: /usr/include/SFML /usr/share/SFML
```

/usr/share/SFML should contains a cmake folder

```
cd /usr/share/SFML/cmake/Modules/
```
check the FindSFML.cmake file.

If there is no cmake and Moduels folders or the FindSFML.cmake does not exist, please create the folders and copy there the file.
Here you can find the correct FindSFML.cmake file https://github.com/SFML/SFML-Game-Development-Book/blob/master/CMake/FindSFML.cmake

### SFML 2.5 section

According to this link: https://en.sfml-dev.org/forums/index.php?topic=24070.0 you should modify the **CMakeLists.txt** files.

The **project root folder CMakeLists.txt** should looks like this:
```
cmake_minimum_required(VERSION 3.2)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(SFML_DIR "/usr/include/SFML/lib/cmake/SFML")

find_package(SFML COMPONENTS graphics system REQUIRED)

include_directories(src)

add_subdirectory(src)
```

The **src folder CMakeLists.txt** should look like this:
```
set(SOURCES
        main.cpp
        gameobject.cpp
        ship.cpp
        bullet.cpp
        game.cpp
        asteroid.cpp
        )

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(gitsteroid ${SOURCES})

target_link_libraries(gitsteroid sfml-graphics sfml-system)
```
