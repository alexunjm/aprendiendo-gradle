# Usos con Docker

## para probar rápidamente gradle desde un contenedor

    docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project gradle gradle <gradle-task>

### flags

    --rm                             Automatically remove the container when it exits
    -u, --user string                Username or UID (format: <name|uid>[:<group|gid>])
    -v, --volume list                Bind mount a volume
    -w, --workdir string             Working directory inside the container

## ejemplos

    docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project gradle gradle tasks --all

    docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project gradle gradle hello

## Detach del container -d

para levantar un contenedor de gradle y utilizar posteriormente desde terminal bash del contenedor

    docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project -d alex/gradle-cpp:1.0 tail -f /dev/null
    # o tambien
    docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project -d alex/gradle-cpp:1.0 sleep infinity

### finalmente, se puede ingresar a la terminal de la siguiente forma

    docker exec -it <containerName> /bin/bash

### ejemplo

    CONTAINER_GRADLE=$(docker run --rm -u gradle -v "$PWD":/home/gradle/project -w /home/gradle/project -d alex/gradle-cpp:1.0 sleep infinity)
    docker exec -it "${CONTAINER_GRADLE}" bash

    # inside of container
    gradle <task>

    # fuera del container, parar la ejecución del contenedor
    docker stop "${CONTAINER_GRADLE}"
