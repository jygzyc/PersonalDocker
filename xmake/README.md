# xmake dev env

## build 

1. Change the project directory in `docker-compose.yml`
2. Change the NDK version for your need in `docker-compose.yml`
2. run `docker compose run --rm xmake_builder bash` and build for yourself

## Compile

```bash
# Run in docker
xmake f -p android -a arm64-v8a -m debug # Compiling Android arm64-v8a ELF file

xmake # build
```