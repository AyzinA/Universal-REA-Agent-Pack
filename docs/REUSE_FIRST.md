# Research and reuse before decompilation

Why: using a valid existing source, symbol database, SDK, file-format parser or implementation can save more work than optimizing the decompiler.

## Search ladder

1. Target's own **debug info**, symbol exports, source maps, manifests and installed SDKs.
2. This workspace's `work/` notes, existing code and previous analysis snapshots.
3. Existing app/game projects, original vendor/public source, SDK header, plugin framework, public protocol and file-format documentation.
4. Targeted GitHub/code search by *unique symbol*, string, feature, subsystem, version and architecture. Prefer upstream over forks and mirrors.
5. Only when evidence is missing: new reverse engineering through REA.

## Search recipes

- Native: `"symbolName" ABI`, `"unique error string" source`, `"product name" SDK symbols`, `"filename.dll" reverse engineering`.
- Electron: `"ipc-message-name"`, `"package-name" source`, `"app.asar" specific feature`.
- Android/.NET: exact class/method/assembly/package with framework or version.
- Games: original engine name + asset format/module, open-source reimplementations, fan SDK, modding framework, known version.

## Decide whether reuse is valid

For each candidate note: repository URL, pinned commit/tag, license, last-known compatibility, whether it is original source, a clean-room recreation, or a partial approximation, and the specific function/struct/algorithm that saves work. Avoid cargo-cult copying; confirm behavior against the actual target binary/version.

Check license for copying code. Link and cite appropriately; **do not paste proprietary decompiled code or large copyrighted sources into reports**. An unverified community function map is a hint, not proof of an address.

## Reuse decision labels

- **Direct reuse:** compatible source/API and license, verified against target.
- **Adapt:** useful documented algorithm/data format, behavior may differ.
- **Reference only:** helps find symbols/understand design, no verified equivalence.
- **Reject:** wrong version, no credible source, incompatible license or insufficient match.

If you find a direct fit, **stop reverse engineering that component** and invest verification effort only in the interface and integration gaps.

The selective catalog in `references/PROJECTS.md` is a starting point, not a mandate to consult every repository.
