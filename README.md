# Cloud sync runner

Minimal public GitHub Actions launcher for a private data synchronization pipeline.

This repository contains no application source code, personal activity files, private exports, OAuth/session material, or private data. The real application and data repositories remain private.

The workflow:
1. checks out private application code using a repository-scoped read-only token;
2. checks out the private destination repository using a separate repository-scoped write token;
3. restores only an encrypted runtime cache;
4. runs the private synchronization logic with detailed output suppressed from public logs;
5. writes results only to the private destination repository;
6. persists a new encrypted cache only after a successful synchronization.

The generic issue trigger is owner-only. Pull requests and fork events never execute the secret-bearing job.


## Owner-only triggers

- `[run-private-sync]`: Garmin workouts + PHYSIO synchronization.
- `[run-physio-only]`: PHYSIO synchronization only. It reuses cached Garmin bundles and never downloads or updates Garmin workouts; if no prior bundle cache exists, it fails closed.

Both issue triggers are restricted to the repository owner and keep private runtime output suppressed from public logs.


## Fusion summary

Successful Garmin + PHYSIO and PHYSIO-only runs also refresh a Fusion Training Status summary in the private training-data repository. The public runner never publishes recovery scores, training loads, sleep, HRV, heart-rate, or other personal metric values; public issues and logs expose only generic execution state.
