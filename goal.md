# Project Goal and Handoff

Last reviewed: 2026-10-25. Capabilities are based on the current README/docs and source layout. Validate runtime paths before reporting a new release as working.

## Goal
Build a local-first Android AI app that runs chat, still-image generation, and Wan2.1 video generation on-device using the app's bundled Quartz ARM64 runtime and native modules.

## Feature inventory

### Implemented / documented
- On-device chat through Quartz's localhost HTTP/SSE API.
- First-run model guidance, GGUF import from Downloads, device-aware sizing, reloadable app-private chat history, and an online model catalog with an offline fallback.
- Agent tools for contacts, calls, SMS, and explicitly triggered web lookup.
- Camera and system photo-picker input, native image-quality gating, and local generated-media storage.
- Resumable SDXL FP16 model download from the project's host, per-file SHA-256 verification, Quartz validation, and atomic installation.
- On-device 1024×1024 image generation through the Quartz-owned parsing/tokenization/scheduling/operators/memory/Vulkan path.
- On-device Wan2.1 T2V 1.3B video generation on Vulkan; `docs/VIDEO_PIPELINE.md` describes the model pack, handoff, and validation contracts.
- Android build/release scripts and lint/typecheck/security/contract-check commands are documented.

### Partial / needs verification
- The README reports physical-device validation on a Samsung SM-S921B running Android 16; verify the exact hardware/build and relevant logs when changing native inference.
- Model download and engine handoff must retain resumable transfers, SHA-256 verification, atomic installation, and the no-concurrent-heavy-engine constraint.
- Each provider/tool path and native Android module still needs regression testing when its files change.

### Not implemented / release blocker
- A production iOS release is not validated yet. The README explicitly says native iOS code must be compiled and exercised on macOS with Xcode before an iOS release.

## Handoff notes for the next agent
1. Read `docs/VIDEO_PIPELINE.md`, the matching module implementation, and `scripts/test-wan-contract.mjs` before changing video generation.
2. Keep inference on-device; optional web lookups are user-triggered and distinct from model inference.
3. Preserve resumable downloads, hash checks, storage-headroom checks, atomic installation, and serialized chat/image/video engine handoff.
4. For Android changes, run the checks documented in `package.json`, then test the affected path on the target device where feasible.
5. Update this file with real device, Android version, model pack, build/commit, and test outcomes.

## Validation
The README documents `npm run lint`, `npm run typecheck`, `npm run test:security`, and `npm run doctor`; check the current scripts before relying on them. This document does not claim a fresh run.
