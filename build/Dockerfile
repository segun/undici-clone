FROM node:22-alpine3.19@sha256:a20e85826910e797a556dc808e070c582546786be9e82c535ecdacd2358e2a27

ARG UID=1000
ARG GID=1000
ARG BINARYEN_VERSION=116

RUN apk add -U clang lld wasi-sdk
RUN mkdir /home/node/undici

WORKDIR /home/node/undici

RUN wget https://github.com/WebAssembly/binaryen/releases/download/version_$BINARYEN_VERSION/binaryen-version_$BINARYEN_VERSION-x86_64-linux.tar.gz && \
    tar -zxvf binaryen-version_$BINARYEN_VERSION-x86_64-linux.tar.gz binaryen-version_$BINARYEN_VERSION/bin/wasm-opt && \
    mv binaryen-version_$BINARYEN_VERSION/bin/wasm-opt ./ && \
    rm binaryen-version_$BINARYEN_VERSION-x86_64-linux.tar.gz && \
    rm -rf binaryen-version_$BINARYEN_VERSION && \
    chmod +x ./wasm-opt

COPY package.json .

COPY build build
COPY deps deps
COPY lib lib

USER node
