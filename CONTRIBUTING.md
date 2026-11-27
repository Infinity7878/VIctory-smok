# Contributing

This fork focuses on Windows and AMD RDNA 4 compatibility. The RX 9070 XT is
the first test target. Contributions for other hardware are welcome.

## Build and test

Use a Visual Studio Developer PowerShell with the Desktop development with
C++ workload and the Rust toolchain pinned in `rust-toolchain.toml`.

```powershell
cargo build --locked --profile diag -p victory --features diagnostics
cargo test --locked --profile diag -p victory-shader --lib size_tests
cargo test --locked --profile diag -p victory-gpu --lib --features diagnostics texture_
cargo test --locked --profile diag -p victory-gpu --lib --features diagnostics host::card_steps::tests
cargo xtask policy
```

Supply your own compatible title files when testing interactively. Keep them
and the runtime's caches outside the checkout. See the
[asset policy](docs/asset-policy.md) for what belongs in commits and reports.

```powershell
.\scripts\play.ps1 -Exe $TitleExecutable -More @{
    VICTORY_AMBIENT_REFLECT = '1'
    VICTORY_CARD_BUFFERS_MIN_KB = '1024'
    VICTORY_MEMORY_MAP = '0'
    VICTORY_RDNA_FLOAT = '0'
}
```

`VICTORY_LIVE_TEXTURES=1` enables an experimental refresh for title textures
that are rewritten in place. It has run on video planes in the intro. The
in-game phone display still needs an end-to-end check.

## Report and submit changes

Include the commit, operating system, CPU, GPU, driver, memory, console
profile, runtime switches, and the checkpoint where the problem occurs.
For performance changes, compare the same scene with the same inputs and
warmed pipeline cache. Report frame times and slow frames alongside FPS.
Omit usernames, local paths, save files, game assets, and shader dumps.

Open pull requests against this fork with the relevant test results. Keep
experimental renderer switches opt-in until their in-game behavior is verified.

## Upstream work

The RDNA 4 record-count fix builds on
[VIctory PR #55](https://github.com/avatarmanz/VIctory-7900XTX/pull/55), and the
facial animation correction builds on
[PR #114](https://github.com/avatarmanz/VIctory-7900XTX/pull/114). The reflection
cap, copy-back ordering fix, and experimental live texture refresh adapt
[PR #314](https://github.com/avatarmanz/VIctory-7900XTX/pull/314),
[PR #383](https://github.com/avatarmanz/VIctory-7900XTX/pull/383), and
[PR #390](https://github.com/avatarmanz/VIctory-7900XTX/pull/390).
