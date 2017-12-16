# Rust -> WebAssembly -> Docker (Ubuntu)

This repository provides a controlled Ubuntu environment (via Docker) for compiling Rust in to WebAssembly.

## Installation

```shell
docker build -t ubuntu-wasm docker/
```

## Getting Started

In your host machine, run the Docker container. Mount the present working directory to `/var/workspace/`,

```shell
docker run -it -v $PWD/:/var/workspace -p 8081:8081 ubuntu-wasm
```

Compile Rust code within the Docker container:

```shell
rustc +nightly --target wasm32-unknown-unknown -O \
               --crate-type=cdylib src/main.rs \
               -o build/main.big.wasm

wasm-gc build/main.big.wasm build/main.wasm
```

## Running the Docker Container

The a simple local HTTP server to host the contents of the project,

```shell
docker run -p 8081:8081 -v $PWD/:/var/workspace ubuntu-wasm
```

In a browser, [`http://localhost:8081`](http://localhost:8081).
