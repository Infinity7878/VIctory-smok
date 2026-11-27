# VIctory-smok

VIctory-smok is a Windows fork of VIctory focused on AMD RDNA 4 compatibility,
rendering, and frame pacing. It runs with compatible title files supplied by
the user. [Upstream project](https://github.com/avatarmanz/VIctory-7900XTX)

| Branch | Purpose |
| --- | --- |
| [`windows-rdna4`](https://github.com/Infinity7878/VIctory-smok/tree/windows-rdna4) | The build tested on the RX 9070 XT. Start here to build, test, or contribute. |
| `main` | The upstream runtime with this project overview. |

The Windows branch starts from the upstream revision used in testing. The
commit count on that branch reflects how far upstream has advanced since
that revision.

## Test status

On Windows 11 with a Ryzen 7 9800X3D, Radeon RX 9070 XT 16 GB, and 32 GB RAM,
the Series X profile reached the prison guard escort. Tested prison passages
typically ran around 18–20 FPS, with shorter stretches at 23–26 FPS. Facial
animation was observed, and tester feedback confirmed corrected eye shading
and visible ground textures.

The intro still stutters. Blank phone screens and intermittent stretched
polygons remain open. Sustained 60 FPS and later missions are unverified.
[Build instructions and known issues](https://github.com/Infinity7878/VIctory-smok/blob/windows-rdna4/README.md)

## Contribute

Open pull requests against `windows-rdna4`. See the contribution guide for
test commands, reporting guidance, and credits for the adapted fixes.
[Contribution guide](https://github.com/Infinity7878/VIctory-smok/blob/windows-rdna4/CONTRIBUTING.md)

The source is GPL-3.0-or-later. Keep title files, saves, and generated shader
caches outside the checkout. [License](LICENSE) · [Asset policy](docs/asset-policy.md)
