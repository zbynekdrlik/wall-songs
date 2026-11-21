# wall-songs — Project Instructions

## What this project is
wall-songs replaces Resolume on the SNV **songs PC**: a separate Windows computer with its own Resolume ("resolume songs") that drives the LED wall visuals for the live band during songs.

Scope (owner, 21.11.2026): visuals on the LED wall during songs, with transitions, reactions to audio and tempo, text effects and the song lyrics.

## What it is NOT (owner corrections, 21.11.2026)
- Not songplayer. songplayer is only a CG player of YouTube videos.
- Not the other Resolume ("resolume bridge") on the SNV bridge PC, which wall-bridge may replace later. Sermon visuals stay on that other Resolume.
- wall-bridge is the sibling LED-wall project; the two stay separate projects.

## Stack — the house stack, BINDING (owner 21.11.2026)
Owner: "musi to byt podobny projekt ako ine nase rust projekty, web rozhranie, ikonka dole v tray, vykony nizkolatencny graficky engine". This is the DEFAULT, never a freeze. Do not silently pick another technology, and do not silently settle for a weaker one either: at the design step, for each layer the work touches, check from read sources (release notes, crate docs/source, benchmarks) whether a clearly better option exists today (a newer major version, a better crate or engine for this specific need). If one does, propose it on the ticket as a stack upgrade with evidence (what, why better here, cost of moving); the owner decides, and an approved upgrade becomes the house default for every project (owner 21.11.2026: "stack musi byt stale otvoreny aby sa rozvijal k lepsim verziam"). Reference implementations: **wall-bridge** (`zbynekdrlik/wall-bridge`: service + tray + Spout + scanout) and **songplayer** (`zbynekdrlik/songplayer`: `sp-gpu` Direct3D 11 compositor + Spout senders, Leptos UI).

| Layer | Technology |
|---|---|
| Language / layout | Rust, one Cargo workspace with `crates/<prefix>-*` (core, engine, service, tray, …) |
| Graphics engine | Native, low latency: `windows` crate (0.58, as the siblings) Direct3D 11 render/compositor on the GPU; video in/out over Spout (and NDI where needed), as songplayer `sp-gpu` and wall-bridge `wb-spout`; frames paced to the output's vblank like wall-bridge `wb-scanout`. No browser/Electron/web canvas renderer, no game engine. |
| Service / API | `axum` + `tokio`, status at `/api/status`, WebSocket for live control |
| Web UI | Leptos (CSR) compiled to WASM with Trunk, served by the axum service (`rules/rust-web-stack.md`), version shown in the UI |
| Tray | `tray-icon` crate, a `<prefix>-tray` crate like wall-bridge `wb-tray`: status, Open UI, Copy URL, Exit (tray only) (`rules/rust-web-tray.md`) |
| Target / build | Windows songs PC; cross-build on dev1 with `cargo build --release --target x86_64-pc-windows-gnu` (target + mingw are system-wide; never install toolchains in the account) |
| Install / run | Installer registers scheduled tasks (engine at logon, tray, watchdog, update) and logs under `C:\ProgramData\WallSongs\logs`, as wall-bridge does |
| CI / tests | GitHub Actions: fmt + clippy `-D warnings`, unit tests, Windows build, Playwright test of the web UI; deploy + on-box verification on the songs PC |

## Open at project start
- The songs PC itself (address, Resolume version, outputs, inputs for audio/tempo) is not recorded anywhere yet. Find it out with the owner; box access goes through remoteos.
- The product design (how lyrics and tempo arrive, how the operator drives it, which effects first) is this project's first ticket, worked with the owner, INSIDE the stack above.
- The owner calls it an MVP for now: keep the first version small, but on the house stack from line one (MVP = fewer features, never a throwaway technology).

## Branches
Two-branch workflow: `dev` for work, `main` for releases, PR dev → main.

## Playbook router
- (empty: add `.claude/rules/<area>.md` files as areas appear)
