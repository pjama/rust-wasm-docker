FROM ubuntu
MAINTAINER Philip Jama

EXPOSE 8081

RUN apt-get update && \
    apt-get install -y curl gcc python3

RUN curl -L https://sh.rustup.rs | sh -s -- -y --default-toolchain=nightly
ENV PATH=$PATH:~/.cargo/bin

RUN ~/.cargo/bin/rustup update
RUN ~/.cargo/bin/rustup target add wasm32-unknown-unknown --toolchain nightly
RUN ~/.cargo/bin/cargo install --git https://github.com/alexcrichton/wasm-gc

WORKDIR /var/workspace

CMD python3 -m http.server 8081
