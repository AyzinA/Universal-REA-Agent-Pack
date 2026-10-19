# Specialized playbooks (load relevant section only)

## Native desktop or game binary (PE / ELF / Mach-O)

Detect architecture and bitness, image base, imports/exports, RTTI/vtables where applicable, PDB/DWARF/DSYM presence, linked runtime, packed/managed indicators. Follow the feature from entry/handler toward the target, not every virtual method in a class. For ABI work, verify member accesses, register/stack conventions and ownership at machine code level. Keep RVA vs VA vs file offset explicit. Record ASLR/module base during runtime investigations.

For games, check open engine ports, modding SDKs, script VMs and public format parsers before extracting their code. Never assume every game uses the same engine, classes, scene format or threading model.

## .NET / managed PE

First verify CLR metadata (a `.exe` is not necessarily native). Use managed type/member/IL routing and PDB if available. Map event registration, serializers, delegates and async state machines. Only use native decompilation for unmanaged interop/NativeAOT or a real native boundary. Obfuscated type names are weak evidence. Do not assume method order or tokens remain stable across builds.

## Java / Android

Start from manifest/components, packages, activities/services, permissions and exact class/method names. Follow normal Java/Kotlin code via JADX/DEX. Check native libraries separately if JNI is involved. Distinguish resources from executable logic, and app runtime behavior from static interpretation. An APK's package identity/version and signing data matter.

## Electron / browser / web

For installed Electron, inspect manifests, `app.asar`, bundled modules, preload, renderer/main process, IPC and source maps before native add-ons. For websites, limit observation to authorized pages and interactions; avoid indiscriminate crawling or user data collection. Source maps may be absent, inaccurate or belong to another build. For JS graph evidence, store results and query one module/page at a time.

## WASM

Inspect imports, exports, sections and WAT/module structure. Resolve JS<->WASM interfaces and linear-memory layouts carefully. Native pointers are not interchangeable with WASM offsets. Verify behavior via deterministic test vectors where possible.

## Firmware / embedded

Determine container and processor ISA, partition maps, filesystems, byte order and load offsets before analyzing instructions. Do not execute unknown firmware on the host. Treat extracted third-party components as separate artifacts with their own hashes and origins.

## Plugins, hooks, version diffs

Fingerprint the **exact deployed version**; discover exports and stable public extension APIs first. Prefer supported SDK/plugin APIs to invasive hooks. For version comparison, map structural/semantic equivalence independently; copying an address or offset from another release is unsafe. Test one isolated change at a time. Only patch/instrument after authorization.

## Dynamic validation (all formats)

Run only when authorized. Use an isolated profile/VM with snapshots, no real credentials, controlled network, logged inputs and deterministic test cases. For a live target, limit observations to the narrow questioned behavior; do not capture unrelated user data.
