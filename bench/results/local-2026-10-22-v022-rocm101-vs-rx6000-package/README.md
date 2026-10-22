# Local results: Strata v0.2.2 on the RX 6700 XT, ROCm 10.1.0 source build against the RX 6000 engine package

Measured 2026-10-22 on the same machine as the other `local-*` and `2026-10-*` RX 6700 XT folders. The summary, the
conditions and the caveats are in the 0.2.2 entry of `docs/AMD_HIP.md` (RDNA2 section); this folder holds the raw outputs
behind it. Nothing here was run through `strata bench run` or `bench/prompts/standard-v1`.

What the files are (all in `raw/`):

- `source-build-rocm101.output`, `package-as-shipped.output`, `package-aligned.output`: the stdout of each run: two
  200-token answers, then the 35k and 90k cold replays with the server's own timings, and one line of sysfs hardware
  numbers per replay.
- `*.samples`: one row per second during each replay: memory clock (MHz), GPU busy (%), free VRAM (MiB) read from sysfs.
- `replay_oai.py`, `replay_oai_key.py`: the replay script (the second adds the API key header the package image needs).
  The replay cuts (`bfe8ff1d-35k.json`, `bfe8ff1d-90k.json`) are from a private agent session and are not in this folder.
- `source-build-config.json`: the `strata-docker` run settings for the source build. `package-launcher-config.json` and
  `package-aligned-engine.log`: what the package launcher wrote and the engine log of the aligned run (the as-shipped
  run's log was overwritten by the restart; its settings are described in the `docs/AMD_HIP.md` entry).
- `strata-pkg-docker.sh`: the script that started the package image (own data folder, GGUF folder mounted read-only,
  port on 127.0.0.1 only, API key). Do not mount a shared models folder as `/data` for that image: its entrypoint moves
  `/data/models`, `/data/packs` and `/data/mtp` into `/data/Strata-data`.

One run per configuration.
