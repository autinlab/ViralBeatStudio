# ViralBeat Studio

ViralBeat Studio is an interactive, browser-based educational app that lets students explore the icosahedral symmetry of virus capsids by mapping music onto their structure. It runs as a single self-contained HTML page — no build step or server required, just open it in a browser.

Students move through a guided workflow:

1. **Capsid Selection** — Pick a virus from a curated library (AAV, HPV, poliovirus, bacteriophages, plant and insect viruses, and more), each loaded as a real 3D structure from the PDB.
2. **Music Import** — Upload an audio track to pair with the capsid.
3. **The Dancing Capsid** — Assign musical features (beat, instrument, rhythm, dynamics) to the capsid's 2-, 3-, and 5-fold symmetry axes. The audio is analyzed in real time so the structure visibly opens and closes in sync with the music.
4. **Card Creator** — Design a scientific trading card describing the chosen virus.
5. **Save & Share** — Export the session or share it via a link.

The 3D molecular visualization is powered by a custom audio-reactive build of [Mol*](https://molstar.org/), maintained at [corredD/molstar-proto (branch `codex/audio-reactive-animation`)](https://github.com/corredD/molstar-proto/tree/codex/audio-reactive-animation), which drives the capsid animation directly from the music.
