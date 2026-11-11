# Fork origin and provenance

This file records where Onym Core comes from, under what terms, and what this
fork has changed. It is an original Onym Core document.

Onym Core is an independent project. It is not affiliated with, sponsored or
endorsed by the Stellar Development Foundation.

## Upstream

| Item | Value |
| --- | --- |
| Upstream project | Stellar Core |
| Upstream repository | https://github.com/stellar/stellar-core |
| Upstream tag | `v30.0.0` |
| Upstream commit | `0e49751aa9ddf892302cca02cea7f3f5d97df9f1` ("Tx set validity hardening (#5481)", committed 2026-10-09) |
| Upstream ledger protocol version | 30 |
| Upstream license | Apache License, Version 2.0 (`LICENSE-APACHE.txt`, `COPYING`) |
| Upstream copyright | "Copyright 2014-2020 Stellar Development Foundation and contributors" (`COPYING`), plus per-file headers of the form "Copyright YYYY Stellar Development Foundation and contributors" |
| Upstream NOTICE file | None. Upstream ships no `NOTICE` file; its attribution statements live in `COPYING` and in per-file headers. |
| Fork repository | https://github.com/onymchat/onym-core |
| Fork date | 2026-11-11 |
| Onym Core license | GPL-3.0-or-later for the combined work (`LICENSE`, `LICENSE-GPL-3.0.txt`). Upstream files stay Apache-2.0. |

The upstream authors and contributors are recorded in the upstream git
history, which this repository preserves in full. The upstream `AUTHORS` file
is empty and has been left as is.

## Upstream and third-party notices

All upstream legal material is kept unchanged:

- [`COPYING`](./COPYING): the upstream license statement and the restated
  licenses of bundled third-party code (ASIO, Catch, cereal, RapidJSON, fmt,
  JsonCpp, SQLite, SOCI, libsodium, Medida, Tracy, spdlog, and others).
- [`LICENSE-APACHE.txt`](./LICENSE-APACHE.txt): the full Apache License 2.0 text.
- Every upstream per-file copyright header.
- The license files of every bundled library and git submodule under `lib/`
  and `src/rust/soroban/`, and those of the crates in `Cargo.lock`. Upstream
  checks crate licenses with `deny.toml`, which is unchanged.

Onym Core adds a [`NOTICE`](./NOTICE) file that tells Onym additions apart from
the upstream attribution. It invents no upstream attribution requirements. It
only restates the license notices of two bundled components that upstream
`COPYING` omits (`xdrpp`, `gperftools`), taken from their own license files.

## Licensing decisions

These were found during the fork inspection.

1. **`lib/xdrpp` is GPL-3.0-or-later: resolved by licensing Onym Core under
   GPL-3.0-or-later.** `xdrpp`'s `COPYING` (submodule commit
   `a29a1703699ad2b6cb4b28538d6ed4173eacdb60`) grants the public distribution
   under GPLv3 or later. It lets the Stellar Development Foundation relicense
   it, and lets CS244b alumni relicense it under Apache 2.0. Onym Core has
   neither right. `libxdrpp.a` is statically linked into `onym-core`, and the
   `xdrc` compiler generates the XDR C++ headers. On 2026-11-11 the project
   decided to distribute Onym Core as a whole under GPL-3.0-or-later (see
   [`LICENSE`](./LICENSE)). Inherited Stellar Core files keep their Apache-2.0
   headers and terms, which are compatible with GPLv3. Onym's own
   contributions are GPL-3.0-or-later. Every other bundled license (MIT, BSD,
   Boost, ISC, Apache-2.0, Unicode, public domain, and the `deny.toml`
   allow-list for Rust crates) was checked and is GPLv3-compatible.
   Distributors of binaries must provide the Complete Corresponding Source
   (GPLv3 section 6). `onym-core version` prints the license and no-warranty
   notice.
2. **`lib/gperftools` (BSD-3-Clause, Google Inc.)** is missing from upstream
   `COPYING`. Its attribution, and that of `xdrpp`, is added in
   [`NOTICE`](./NOTICE) instead of editing the upstream `COPYING`.
3. **Repository name (resolved).** The fork repository was first created as
   `onymchat/stellar-core`. Because the Stellar Brand Policy restricts the use
   of "Stellar" in project names, it was renamed to `onymchat/onym-core` on
   2026-11-11. GitHub redirects the old URL.

## Scope of the initial modification

The first Onym commit (`chore: initialize Onym Core fork with compliant
attribution and branding`) changes **branding, packaging metadata and
documentation only**. It does not change the ledger protocol, XDR, consensus,
networking, cryptography, persistent formats, configuration semantics or tests.

Every modified upstream file carries a notice saying it was modified by the
Onym Core contributors, as Apache License 2.0 section 4(b) requires. The
changes are:

| File | Change |
| --- | --- |
| `README.md` | Rewritten to identify Onym Core as an independent fork. The upstream Stellar logo and badges are removed. |
| `SECURITY.md` | Points Onym vulnerability reports to Onym maintainers instead of the SDF bug bounty program, which does not cover this fork. |
| `configure.ac` | Autoconf package name `stellar-core` → `onym-core`, package URL → the fork repository. |
| `src/Makefile.am` | Built program `stellar-core` → `onym-core` (automake variables `stellar_core_*` → `onym_core_*`), and the fuzz helper targets that invoke it. |
| `src/test/selftest-parallel`, `src/test/run-selftest-nopg`, `src/test/run-selftest-pg` | Invoke `./onym-core` instead of `./stellar-core`. |
| `docker/Dockerfile.testing` | Copy and run `onym-core` instead of `stellar-core`. |
| `.gitignore` | Ignore the built `src/onym-core`. |
| `src/main/CommandLine.cpp` | Executable name in help and usage text, help descriptions, a log message, and an Onym identification and independence statement printed after the `version` output. |
| `src/main/main.cpp`, `src/main/ApplicationUtils.cpp`, `src/main/ApplicationImpl.cpp`, `src/main/ErrorMessages.h` | Executable name in user-facing log, warning and error messages. |
| `src/main/CommandHandler.cpp` | HTTP root page says "Welcome to onym-core!" and carries the independence statement. |

New files: `FORK_ORIGIN.md`, `NOTICE`, `TRADEMARKS.md`.

A second commit (`chore: license Onym Core under GPL-3.0-or-later`) makes the
licensing decision described above. It adds `LICENSE` and the verbatim
`LICENSE-GPL-3.0.txt` (from https://www.gnu.org/licenses/gpl-3.0.txt, SHA-256
`3972dc9744f6499f0f9b2dbf76696f2ae7ad8af9b23dde66d6af86c9dfb36986`), updates
`NOTICE`, `README.md` and this file, and adds the license and no-warranty
notice to the `onym-core version` output (`src/main/CommandLine.cpp`). Like
the first commit, it changes no protocol or runtime behavior.

## Deliberately unchanged identifiers

These upstream names remain, because renaming them could change protocol,
network, storage or tooling behavior, or would make this commit larger than a
reviewable branding baseline. Each will be revisited, if at all, in a separate
commit.

| Identifier | Why it is unchanged |
| --- | --- |
| Network passphrases (`"Public Global Stellar Network ; September 2015"`, `"Test SDF Network ; September 2015"`) and network IDs derived from them | They define network identity and transaction signatures. Changing them is a protocol and genesis decision. |
| XDR definitions (`src/protocol-curr/xdr`, the `stellar` XDR namespace, `rs-stellar-xdr`) | They define the wire and hash format. |
| C++ namespace `stellar` | It is used throughout the code and in generated XDR code. Renaming it has no effect on users and touches every file. |
| `STELLAR_CORE_VERSION`, `StellarCoreVersion.cpp.in`, `getStellarCoreMajorReleaseVersion` | Internal symbols. The version string itself is generated by `git describe` and is sent to peers in the overlay `HELLO` message. |
| Rust crate `stellar-core` and static library `rust_stellar_core` (`src/rust/Cargo.toml`, `Cargo.lock`, `src/Makefile.am`) | Renaming them changes `Cargo.lock` and the dependency-tree checks under `src/rust/src/dep-trees`. Deferred to keep this commit small. |
| Soroban host crates (`soroban-env-host`, `rs-soroban-env` submodules) | They define smart-contract execution semantics. They are external dependencies. |
| History archive layout (`.well-known/stellar-history.json`, `stellar-history.json`) | It is part of the history archive format that other nodes and tools read. |
| Default configuration file name `stellar-core.cfg`, default log file name `stellar-core-{datetime}.log`, `docs/stellar-core_*.cfg` example files and their test copies in `src/testdata/` | Changing the defaults changes behavior for existing deployments, and tests load the example files by name. |
| Database names (for example the `stellar` misc database name) and schema | Persistent storage format. |
| Environment variables such as `STELLAR_CORE_TEST_PARAMS` | They are used by test scripts and CI. |
| `stellar-core.supp` (valgrind suppressions) | A build-internal file name. |
| `docker/Dockerfile`, `docker/Makefile` | They install and tag the **official SDF** `stellar-core` package and image. They must be replaced, not renamed, once Onym has its own packages. Until then they should not be used for Onym releases. |
| `Builds/VisualStudio/*` | The Windows build is not maintained or tested in this fork yet. |
| `.github/workflows/*`, `ci-build.sh` | Upstream CI targets SDF's runner pool and won't run unchanged in this fork. |
| Inherited technical documentation (`docs/`, `INSTALL.md`, `CONTRIBUTING.md`, `src/**/README.md`, `.claude/`, `.github/` templates) | It describes behavior that is still identical to upstream. It is left as is and will be updated as Onym's behavior diverges. |
| Release-tag and protocol version coupling (`checkStellarCoreMajorVersionProtocolIdentity` in `src/main/main.cpp`) | A release-tagged build (`vX.Y.Z`) refuses to start unless `X` equals the ledger protocol version. Onym release tags must follow this scheme, or the check must be changed deliberately. |

## Independent status

Onym Core is maintained independently of the Stellar Development Foundation.
Changes made here are not reviewed, endorsed or supported by the Stellar
Development Foundation, and upstream security fixes have to be merged into
this fork by its maintainers.
