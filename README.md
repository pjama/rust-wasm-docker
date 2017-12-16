# Rust -> WebAssembly -> Docker (Ubuntu)

A controlled Ubuntu environment (Docker) for compiling Rust in to WebAssembly.

## Installation

```shell
docker build -t ubuntu-wasm docker/
```

## Getting Started

In your host machine, run the Docker container.


```shell
docker run -it -v $PWD/:/var/workspace -p 8081:8081 ubuntu-wasm /bin/bash
```

_(Mounts the present working directory to `/var/workspace/` and runs `bash`.)_

**Compile** Rust code within the Docker container:

```shell
rustc +nightly --target wasm32-unknown-unknown -O \
               --crate-type=cdylib src/main.rs \
               -o build/main.big.wasm

wasm-gc build/main.big.wasm build/main.wasm
```

## Running the Docker Container

The Docker container runs a local HTTP server to host the local contents,

```shell
docker run -p 8081:8081 -v $PWD/:/var/workspace ubuntu-wasm
```

In a browser, [`http://localhost:8081`](http://localhost:8081).
