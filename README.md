# Cabby releases

Downloads for Cabby. Pick a version on the [Releases](https://github.com/DaniG2k/cabby-releases/releases) page.
This repository holds release files only.

## What is Cabby?

Cabby is a real-time WebSocket server written in Rust. It holds the WebSocket connections for
Rails (Action Cable), Laravel, Node.js and Django apps, so your app doesn't have to. It is
compatible with AnyCable clients.

Documentation: https://docs.cabbyhq.com/install

## Quick start

### Binary

Builds are available for Linux (x86_64 and arm64, glibc 2.28 or newer) and macOS (Apple
silicon). Download a tarball and `SHA256SUMS` from
https://github.com/DaniG2k/cabby-releases/releases, then:

```sh
shasum -a 256 -c SHA256SUMS --ignore-missing
tar -xzf cabby-0.2.0-x86_64-unknown-linux-gnu.tar.gz
./cabby --version
./cabby --norpc --public --broadcast_adapter=http
```

The default broadcast adapters are `http,redis`, so a standalone binary needs
`--broadcast_adapter=http` unless Redis is running on `localhost:6379`.

### Docker

```sh
docker run --rm -p 8080:8080 -p 8090:8090 ghcr.io/danig2k/cabby:0.2.0 --norpc --public
```

The image listens on `0.0.0.0` and uses the HTTP broadcast adapter, so it runs without Redis.
Configure it with flags or `CABBY_*` environment variables (`-e`); `ANYCABLE_*` names still work.

### Try it

`--public` accepts every connection and subscription without authentication, so use it only
locally. Clients connect to `ws://localhost:8080/cable`. Broadcast to a stream with:

```sh
curl -X POST localhost:8090/_broadcast -H 'Content-Type: application/json' \
  -d '{"stream":"demo","data":"{\"text\":\"hello\"}"}'
```

`cabby --help` lists every flag and its environment variable.

## License

Cabby is released under the MIT License. `LICENSE` also includes AnyCable's MIT notice, because
Cabby is derived from AnyCable. The licenses of the Rust crates in the binary are in
`THIRD_PARTY_LICENSES.md`.

## Source code

https://github.com/DaniG2k/cabby
