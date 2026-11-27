# VIctory-smok for Windows

VIctory-smok is a Windows build of the VIctory compatibility layer with fixes
tested on AMD RDNA 4. The `windows-rdna4` branch builds from upstream revision
`e2a28ec`, the base used for the test results below.
[Upstream project](https://github.com/avatarmanz/VIctory-7900XTX)

## Test status

The test PC had Windows 11, a Ryzen 7 9800X3D, Radeon RX 9070 XT 16 GB, and 32 GB
RAM. Tests used the Series X profile, ray tracing off, and a warmed pipeline
cache. Results are from the prologue and prison.

| Area | Observed result |
| --- | --- |
| Progression | Reached the guard escort through the prison hallway. Later missions are unverified. |
| Frame rate | Usually 18–20 FPS during the tested prison sequences, with short stretches at 23–26 FPS. The intro still has stalls. |
| Characters | Lip, jaw, and blink animation observed. The tester confirmed corrected eye shading. |
| Ground and geometry | The tester confirmed visible ground textures. Intermittent stretched polygons remain open. |
| Phone displays | Blank screens remain open. The experimental texture refresh ran on intro video textures. |
| 60 FPS | Still a target. The tested title requested a 33.3 ms frame interval. |

## Build and run

Use Windows 10 or 11 x64, an AVX2-capable CPU, a Direct3D 12 GPU with shader
model 6.6 and mesh shader support, the pinned Rust toolchain, and the Visual
Studio C++ build tools. Supply your own compatible title files and store
them outside this checkout.

From a Visual Studio Developer PowerShell:

```powershell
git clone --branch windows-rdna4 https://github.com/Infinity7878/VIctory-smok.git
Set-Location VIctory-smok
Copy-Item victory.example.toml victory.toml
cargo build --locked --profile diag -p victory --features diagnostics
```

In `victory.toml`, set `game_dir` to the directory containing your title
files. Set `$TitleExecutable` to the full path of the title executable
before running:

```powershell
.\scripts\play.ps1 -Exe $TitleExecutable -More @{
    VICTORY_AMBIENT_REFLECT = '1'
    VICTORY_CARD_BUFFERS_MIN_KB = '1024'
    VICTORY_DISPLAY_MODE = '1920x1080'
    VICTORY_MEMORY_MAP = '0'
    VICTORY_RDNA_FLOAT = '0'
    VICTORY_SLOT_COUNTS = '1'
    VICTORY_TEXTURE_ROOM_PERCENT = '78'
    VICTORY_WINDOW_MAX = '1280x720'
}
```

`VICTORY_DISPLAY_MODE` controls the reported display mode. The game still
drew world frames at 2560×1440 in the tested configuration. After a run,
`.\target\diag\victory.exe warm --used` prebuilds pipelines observed in that
cache. Streaming and frame-pacing stalls can still occur.

## Contribute

Target `windows-rdna4` for pull requests about this build. Include the
hardware, driver, settings, test scene, and frame times in performance
reports. [Test commands and credits](CONTRIBUTING.md)

The source is GPL-3.0-or-later. Title files, saves, and generated shader
caches belong outside the checkout. [License](LICENSE) · [Asset policy](docs/asset-policy.md)
