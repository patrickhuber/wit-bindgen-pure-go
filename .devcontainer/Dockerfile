FROM mcr.microsoft.com/devcontainers/base:jammy

# these must be after the FROM clause or they are removed
ARG WASMTOOLS_VERSION=1.0.38
ARG WITBINDGEN_VERSION=0.9.0
ARG TINYGO_VERSION=0.28.1

RUN wget https://github.com/bytecodealliance/wasm-tools/releases/download/wasm-tools-${WASMTOOLS_VERSION}/wasm-tools-${WASMTOOLS_VERSION}-x86_64-linux.tar.gz -O ${HOME}/wasm-tools-${WASMTOOLS_VERSION}-x86_64-linux.tar.gz
RUN wget https://github.com/bytecodealliance/wit-bindgen/releases/download/wit-bindgen-cli-${WITBINDGEN_VERSION}/wit-bindgen-v${WITBINDGEN_VERSION}-x86_64-linux.tar.gz -O ${HOME}/wit-bindgen-v${WITBINDGEN_VERSION}-x86_64-linux.tar.gz
RUN wget https://github.com/tinygo-org/tinygo/releases/download/v${TINYGO_VERSION}/tinygo_${TINYGO_VERSION}_amd64.deb -O ${HOME}/tinygo_${TINYGO_VERSION}_amd64.deb && \
dpkg -i ${HOME}/tinygo_${TINYGO_VERSION}_amd64.deb
RUN tar -xf ${HOME}/wasm-tools-${WASMTOOLS_VERSION}-x86_64-linux.tar.gz -C ${HOME}/ wasm-tools-${WASMTOOLS_VERSION}-x86_64-linux/wasm-tools
RUN tar -xf ${HOME}/wit-bindgen-v${WITBINDGEN_VERSION}-x86_64-linux.tar.gz  -C ${HOME}/ wit-bindgen-v${WITBINDGEN_VERSION}-x86_64-linux/wit-bindgen
RUN mv ${HOME}/wasm-tools-${WASMTOOLS_VERSION}-x86_64-linux/wasm-tools /usr/local/bin
RUN mv ${HOME}/wit-bindgen-v${WITBINDGEN_VERSION}-x86_64-linux/wit-bindgen /usr/local/bin 