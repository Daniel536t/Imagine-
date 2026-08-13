# MMT V3 Core — Security Heist Board

This repository contains the visual security map created during the authorized local review of the MMT V3 Core Move packages.

## Files

- [`HEIST_BOARD.svg`](./HEIST_BOARD.svg) — the downloadable vector illustration of the bank, perimeter, vault, guards, alarms, and protocol rooms.
- [`HEIST_BOARD_LEGEND.md`](./HEIST_BOARD_LEGEND.md) — the complete numbered inventory and explanation of the represented objects.
- [`HEIST_REPLAY.html`](./HEIST_REPLAY.html) — a Three.js CDN-powered 3D fictional audit replay with cameras, scenarios, alarms, and trace evidence.

Open `HEIST_REPLAY.html` in a browser with internet access to load the Three.js modules. Choose a scenario, switch cameras, and press **Run**.

The SVG can be opened directly in a browser or downloaded from GitHub. It is self-contained and has no external image dependencies.

Review status at export time:

- `clmm`: 364/364 Move tests passed.
- `slippage_check`: compiled successfully after dependency cleanup; it currently contains 0 tests.
