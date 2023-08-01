# Dev Container Build Instructions

When the devcontainer is started the following depenencies are installed:

* go 
* tiny-go
* rust
* wasm-tools 
* wit-bindgen

To run the sample, run the following commands:

# go wasm guest component

## build

```bash
export GO_EXAMPLE=go_example
pushd go-example
tinygo build -target=wasi -o ${GO_EXAMPLE}.wasm main.go
mv ${GO_EXAMPLE}.wasm ../${GO_EXAMPLE}.wasm
popd
```

## generate

```bash
# download the wasm snapshot
wget https://github.com/bytecodealliance/wasmtime/releases/download/dev/wasi_snapshot_preview1.reactor.wasm
wasm-tools component embed ./go-example/wit/host.wit ${GO_EXAMPLE}.wasm -o embed.${GO_EXAMPLE}.wasm
wasm-tools component new embed.${GO_EXAMPLE}.wasm -o component.${GO_EXAMPLE}.wasm --adapt wasi_snapshot_preview1=./wasi_snapshot_preview1.reactor.wasm
wasm-tools component wit component.${GO_EXAMPLE}.wasm
```

# build the rust wasm host

## build

```bash
pushd host 
cargo build --release 
mv ./target/release/host ../bin/host
popd
```

## run 

```bash
./bin/host ./component.${GO_EXAMPLE}.wasm
```