# llvm-prebuilt

Prebuilt LLVM-C shared library (`LLVM.dll`) for use by [dasLLVM](https://github.com/GaijinEntertainment/daScript/tree/master/modules/dasLLVM).

Each release ships one tarball per platform containing a single `LLVM.dll`
(renamed from `libLLVM.so.*` / `libLLVM.dylib` / `LLVM-C.dll`).
Windows tarball additionally contains `clang-cl.exe`.

## Platforms

| Tarball | Source |
|---------|--------|
| `linux_64_llvm.tar.gz` | `apt.llvm.org` on `ubuntu-22.04` |
| `linux_arm64_llvm.tar.gz` | `apt.llvm.org` on `ubuntu-22.04-arm` |
| `mac_64_llvm.tar.gz` | `brew install llvm@N` on `macos-13` (Intel) |
| `mac_arm64_llvm.tar.gz` | `brew install llvm@N` on `macos-14` (Apple Silicon) |
| `win64_llvm.tar.gz` | Official `LLVM-N.M.K-win64.exe` (`LLVM-C.dll` + `clang-cl.exe`) |

## Building a new release

1. Push the workflow change.
2. GitHub → Actions → **build-llvm** → **Run workflow**.
3. Inputs: `llvm_version` (e.g. `22.1.5`), `llvm_major` (e.g. `22`).
4. Job creates a **draft release** `v<version>` with all 5 tarballs + `SHA256SUMS`.
5. Edit the draft, publish.

## Consumer

`modules/dasLLVM/CMakeLists.txt` in daScript pins the version + per-platform sha256.
After publishing, update both there.
