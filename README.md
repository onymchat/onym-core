<!--
Modified by the Onym Core contributors in 2026: rewritten to identify this
repository as Onym Core, an independent fork of Stellar Core. The upstream
README is available at https://github.com/stellar/stellar-core/blob/v30.0.0/README.md.
-->

# Onym Core

Onym Core is an independent open-source blockchain implementation forked from
Stellar Core.

> This is independent software, not affiliated with, sponsored or endorsed by
> the Stellar Development Foundation.

Onym Core is derived from [Stellar Core](https://github.com/stellar/stellar-core)
(upstream tag `v30.0.0`, commit `0e49751aa9ddf892302cca02cea7f3f5d97df9f1`),
which is developed by the Stellar Development Foundation and contributors and
licensed under the Apache License, Version 2.0. See
[FORK_ORIGIN.md](./FORK_ORIGIN.md) for the full provenance record and
[TRADEMARKS.md](./TRADEMARKS.md) for how upstream names are used here.

## What it is

Onym Core is a replicated state machine that maintains a local copy of a
cryptographic ledger and processes transactions against it, in consensus with a
set of peers, using the federated Stellar Consensus Protocol (SCP) inherited
from upstream. It is written in C++20 and Rust.

The node executable is `onym-core`.

## Current status

This revision is a branding and licensing baseline only. Its ledger protocol,
transaction format, consensus rules and network behavior are **identical to
upstream Stellar Core v30.0.0**. In particular, the bundled configuration
examples still target the Stellar public network and testnet, and the code
still uses upstream identifiers (for example the `stellar` C++ namespace, the
`stellar-core.cfg` default configuration file name and the
`STELLAR_CORE_VERSION` macro) where renaming them could affect
compatibility. These are listed in [FORK_ORIGIN.md](./FORK_ORIGIN.md#deliberately-unchanged-identifiers).

## Documentation

Most technical documentation in [`./docs`](./docs) is inherited from upstream
and still describes the software as `stellar-core`. Unless noted otherwise,
read `stellar-core` there as `onym-core` for the executable name.

- [Installation](./INSTALL.md) (the built executable is `src/onym-core`)
- [Contributing](./CONTRIBUTING.md)
- [Running tests](./CONTRIBUTING.md#running-tests)
- [Security policy](./SECURITY.md)

## Quick start

```sh
git submodule update --init --recursive
./autogen.sh
./configure
make -j"$(nproc 2>/dev/null || sysctl -n hw.ncpu)"
./src/onym-core version
```

## License

Onym Core is distributed under the Apache License, Version 2.0, as was the
upstream work it is derived from. See [COPYING](./COPYING),
[LICENSE-APACHE.txt](./LICENSE-APACHE.txt) and [NOTICE](./NOTICE). Bundled
third-party libraries are under their own licenses, listed in
[COPYING](./COPYING) and in each library's directory under `lib/`.

**Open licensing issue:** the bundled `lib/xdrpp` submodule, which is
statically linked into `onym-core`, is licensed GPL-3.0-or-later (see
[`lib/xdrpp/COPYING`](https://github.com/xdrpp/xdrpp/blob/master/COPYING)), and
upstream `COPYING` does not list it. See
[FORK_ORIGIN.md](./FORK_ORIGIN.md#open-licensing-issues) before distributing
binaries.

"Stellar" is a trademark of the Stellar Development Foundation. All rights
reserved.
