# Estructura de archivos y carpetas

    ├── gradle [1]
    │   └── wrapper
    │       ├── gradle-wrapper.jar
    │       └── gradle-wrapper.properties
    ├── gradlew [2]
    ├── gradlew.bat [2]
    ├── settings.gradle [3]
    └── app
        ├── build.gradle [4]
        └── src
            ├── main
            │   └── cpp [5]
            │   │   └── app.cpp
            │   └── headers
            │       └── app.h
            └── test
                └── cpp [6]
                    └── app_test.cpp

1. Generated folder for wrapper files
2. Gradle wrapper start scripts
3. Settings file to define build name and subprojects
4. Build script of app project
5. Default C++ source folder
6. Default C++ test source folder

# 3. settings.gradle

    settings.gradle
    rootProject.name = 'demo'
    include('app')

rootProject.name assigns a name to the build, which overrides the default behavior of naming the build after the directory it’s in. It’s recommended to set a fixed name as the folder might change if the project is shared - e.g. as root of a Git repository.

include("app") defines that the build consists of one subproject called app that contains the actual code and build logic. More subprojects can be added by additional include(…​) statements.

# 4. app/build.gradle

    plugins {
        id 'cpp-application' [1]

        id 'cpp-unit-test' [2]
    }

    application { [3]
        targetMachines.add(machines.linux.x86_64)
    }

1. Apply the cpp-application plugin to add support for building C++ executables
2. Apply the cpp-unit-test plugin to add support for building and running C++ test executables

## 5. y 6. son un ejemplo de código probado

# Build de la aplicación

## Construir imagen docker

    docker build -t alex/gradle-cpp:1.0 .


    # inside of container
    ./gradlew build

## Carpeta de salida de compilación

    ./app/build/install
    ├── main
    │   └── debug
    │       ├── app [1]
    │       └── lib
    │           └── app [2]
    └── test
        ├── appTest [1]
        └── lib
            └── appTest [3]

1. The script for executing the application variant
2. The main executable binary (debug variant)
3. The test executable binary

# Correr la aplicación

    ./app/build/exe/main/debug/app
    # output
    # Hello, World!
