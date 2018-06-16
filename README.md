## Dependencies
* cmake
* make
* g++ <with c++11 support>
* sfml (2.4, 2.5 tested)

## Build & Run

**NOTE: SFML 2.5 handles CMake on a different way than 2.4.**

### Install SFML to your computer
https://www.sfml-dev.org/tutorials/2.5/start-linux.php

### SFML 2.5 section

If you installed SFML 2.5 to your system than you can easily compile and run the game with these commands.

```
# build
take build
cmake ..
make

# run
cd build/src
./asteroid
```


#### Preferred to run this stuff in docker

If your system's package manager does not able to install SFML 2.5 or you just prefer using, docker than you can use the following command.

**NOTE At the moment you can not run the binary inside the docker container but this is my next task.**

```
docker run --rm -it -v <source-directory>:/source norbertfenk/asteroid bash
```
Inside the container you should run the same commands as above.

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

If you want to build the project with SFML 2.4 you should do the following changes.

Modify the root CMakeLists.txt this way:
```
cmake_minimum_required(VERSION 3.9)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_MODULE_PATH "/usr/share/SFML/cmake/Modules" ${CMAKE_MODULE_PATH})
find_package(SFML REQUIRED system window graphics)

add_subdirectory(src)

```
Modify the src/CMakeLists.txt this way:
```
set(SOURCES
        <copy-every-cpp-filename-here>
)

include_directories(${CMAKE_CURRENT_SOURCE_DIR})

add_executable(asteroid ${SOURCES})

include_directories(${SFML_INCLUDE_DIR})
target_link_libraries(asteroid ${SFML_LIBRARIES})
```
