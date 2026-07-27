A utility to fetch or build patched Node binaries used by [pkg](https://github.com/sunjingyun/pkg) to generate executables.

## Patched Node versions

Exact Node versions with patches under `patches/` (aliases such as `node24` resolve to the newest matching entry):

| Version   | Notes                                                                                                                                               |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| v24.18.0  | Supported. Loader patches follow Node 22+/24 (`package_json_reader.read` + `cjs/loader.stat` via patched `fs`) so snapshot module resolution works. |
| v20.20.0  | Supported / previously verified                                                                                                                     |
| v20.10.0  | Supported / previously verified                                                                                                                     |
| v19.8.1   | Legacy                                                                                                                                              |
| v18.18.2  | Legacy                                                                                                                                              |
| v16.20.2  | Legacy                                                                                                                                              |
| v14.21.3  | Legacy                                                                                                                                              |
| v12.22.11 | Legacy                                                                                                                                              |
| v10.24.1  | Legacy                                                                                                                                              |
| v8.17.0   | Legacy                                                                                                                                              |

`node24` / `latest` currently resolve to **v24.18.0**. Example:

```sh
pkg-fetch --node-range node24.18.0 --platform linux --arch x64 --force-build --test
```

## Binary Compatibility

| Node                                                                                                                                                       | Platform    | Architectures             | Minimum OS version                                                                |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------------------------- | --------------------------------------------------------------------------------- |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18                                  | alpine      | x64, arm64                | 3.7.3, other distros with musl libc >= 1.1.18                                     |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18, 20, 24.18.0<sup>[4](#fn4)</sup> | linux       | x64                       | Enterprise Linux 7, Ubuntu 14.04, Debian jessie, other distros with glibc >= 2.17 |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18                                  | linux       | arm64                     | Enterprise Linux 8, Ubuntu 18.04, Debian buster, other distros with glibc >= 2.27 |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18                                  | linuxstatic | x64, arm64                | Any distro with Linux Kernel >= 2.6.32 (>= 3.10 strongly recommended)             |
| 16<sup>[1](#fn1)</sup>, 18, 20                                                                                                                             | linuxstatic | armv7<sup>[2](#fn2)</sup> | Any distro with Linux Kernel >= 2.6.32 (>= 3.10 strongly recommended)             |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18                                  | macos       | x64                       | 10.13                                                                             |
| 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18, 20                                                                                                     | macos       | arm64<sup>[3](#fn3)</sup> | 11.0                                                                              |
| 8<sup>[1](#fn1)</sup>, 10<sup>[1](#fn1)</sup>, 12<sup>[1](#fn1)</sup>, 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18                                  | win         | x64                       | 8.1                                                                               |
| 14<sup>[1](#fn1)</sup>, 16<sup>[1](#fn1)</sup>, 18, 20                                                                                                     | win         | arm64                     | 10                                                                                |

<em id="fn1">[1]</em>: end-of-life, may be removed in the next major release.

<em id="fn2">[2]</em>: best-effort basis, not semver-protected.

<em id="fn3">[3]</em>: [mandatory code signing](https://developer.apple.com/documentation/macos-release-notes/macos-big-sur-11_0_1-universal-apps-release-notes) is enforced by Apple.

<em id="fn4">[4]</em>: Patched as **v24.18.0**. Verified by building and packaging on Debian 12 (bookworm) / glibc, host Ubuntu 24.04.
