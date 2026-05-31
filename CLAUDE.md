# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is currently a **stub**: it contains only `README.md`, `LICENSE`, and the initial commit — no application code, package manifest, or build configuration yet. The sections below describe the **intended** product and architecture so that future work stays consistent with the design goals. Verify what actually exists before assuming a file or command is present.

## What ViralBeat Studio is

An interactive, browser-based educational app for exploring the icosahedral symmetry of virus capsids by mapping music onto their structure. Core constraint: it ships as a **single self-contained HTML page** — **no build step and no server**. Development and testing are done by opening the HTML file directly in a browser. Preserve this property; do not introduce a bundler, package manager, or server requirement without an explicit decision to change the deployment model.

## Running / developing

There is no build, lint, or test tooling. To run the app, open the main HTML file in a browser (e.g. `open <main>.html` on macOS). Because there is no transpile/bundle step, edits to the HTML/JS/CSS are reflected on page reload.

## Architecture

The app is structured as a guided 5-step workflow. Each step is a stage in the same single-page session, sharing state (selected capsid, imported audio, axis-to-feature mappings, card content):

1. **Capsid Selection** — Pick a virus from a curated library (AAV, HPV, poliovirus, bacteriophages, plant/insect viruses, etc.). Each entry loads a real 3D structure from the PDB.
2. **Music Import** — Upload an audio track to pair with the capsid.
3. **The Dancing Capsid** — Assign musical features (beat, instrument, rhythm, dynamics) to the capsid's **2-, 3-, and 5-fold icosahedral symmetry axes**. Audio is analyzed in real time so the structure opens and closes in sync with the music.
4. **Card Creator** — Design a scientific trading card describing the virus.
5. **Save & Share** — Export the session or share it via a link.

### Key dependency: audio-reactive Mol*

The 3D molecular visualization is **not** stock Mol* (https://molstar.org/). It is a **custom audio-reactive build** maintained at `corredD/molstar-proto`, branch **`codex/audio-reactive-animation`** (https://github.com/corredD/molstar-proto/tree/codex/audio-reactive-animation). This fork is what drives the capsid animation directly from the music. When working on the "Dancing Capsid" step, the integration point is this fork's audio-reactive animation API — changes to capsid motion belong there or in how the page feeds analyzed audio into it, not in a reimplementation.

The conceptual data flow for the animation: imported audio → real-time analysis (beat/instrument/rhythm/dynamics) → user-defined mapping onto 2/3/5-fold symmetry axes → audio-reactive Mol* opens/closes the capsid along those axes.
