# Example reusable TASK.md objectives

## Windows desktop software

- Target: `C:\\Program Files\\Example\\Example.exe`
- Question: `Trace how the application stores user preferences; identify serializer format and error handling.`
- Deliverable: `analysis`
- Acceptance criteria: `2 supported call-path locations and a small mock serialization test if feasible.`
- Permissions: `read-only static inspection`

## Electron application

- Target: `/opt/Example/resources/app.asar`
- Question: `Map how a specific menu action crosses renderer/preload/main IPC and calls a native addon, if any.`
- Deliverable: `analysis`
- Acceptance criteria: `message identifier, relevant modules, observed data contract, or a clear unknown.`

## Game engine

- Target: `D:\\Games\\Example\\Engine.exe`
- Question: `Map animation event dispatch and verify the memory layout of the event object for this exact build.`
- Deliverable: `plugin interface analysis`
- Acceptance criteria: `verified dispatch call sites, offsets, architecture and ABI; no executable hook unless separately requested.`

## Android app

- Target: `/home/user/artifacts/example.apk`
- Question: `Explain how offline article cache invalidation works, including file/database stores.`
- Deliverable: `analysis`
- Acceptance criteria: `class/method evidence for trigger and storage path; limits disclosed.`

## Linux crash

- Target: `/home/user/bin/example`
- Question: `Identify the probable cause of a known crash at module-relative offset 0x1234 in the supplied build.`
- Deliverable: `bug analysis`
- Acceptance criteria: `correct address mapping, call sites, minimal reproducible condition or unknown.`
