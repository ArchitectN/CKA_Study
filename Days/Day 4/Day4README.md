CMD vs ENTRYPOINT & Few Important Commands

1.  CMD vs ENTRYPOINT
CMD is an executable command at startup that can be overwritten when you append a command

ENTRYPOINT is used to always run at startup and commands added will be appended


2. Dockerfile names & build context
docker build -f ec -t ec-image .
    -f: can be used to specify which docker image to use
    -t: tag the build name


3. Important docker commands
docker container prune
    deletes all stopped containers


docker run vs docker start
run: creates a **new** container from an image
start: restarts an **existing (stopped)** container

--help

used for syntax help to complete a COMMAND

docker remove
used to remove a specific image or container