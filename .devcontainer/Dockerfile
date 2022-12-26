FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive \
    apt-get install -y \
    build-essential \
    git \
    m4 \
    unzip \
    curl \
    pkg-config \
    ocaml \
    opam \
    && rm -rf /var/lib/apt/lists/*

USER vscode
RUN opam init -y --disable-sandboxing && \
    eval $(opam env) && \
    opam repository add satysfi-external https://github.com/gfngfn/satysfi-external-repo.git && \
    opam repository add satyrographos https://github.com/na4zagin3/satyrographos-repo.git && \
    opam update

RUN opam install -y opam-depext && \
    opam depext -y satysfi satysfi-dist satyrographos && \
    opam install -y satysfi satysfi-dist satyrographos && \
    eval $(opam env) && \
    satyrographos install

RUN echo 'eval $(opam env)' >> ~/.profile

RUN cd && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > install_rust.sh && \
    sh install_rust.sh -y && \
    rm install_rust.sh

RUN . "$HOME/.cargo/env" && cargo install --git https://github.com/monaqa/satysfi-language-server
