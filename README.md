<img src="https://storage.googleapis.com/kpt-dev/docs/logo.png" width="50" height="50" />

# KPT

kpt is a toolkit to help you manage, manipulate, customize, and apply Kubernetes Resource configuration data files.

- Fetch, update, and sync configuration files using git.
- Examine and modify configuration files.
- Generate, transform, validate configuration files using containerized functions.
- Apply configuration files to clusters.

## Installation

### Install with Gcloud

The version of kpt installed using `gcloud` may not be the latest released version.

```Shell
gcloud components install kpt
```

### Install with Homebrew

```Shell
brew tap GoogleContainerTools/kpt https://github.com/GoogleContainerTools/kpt.git
brew install kpt
```

### Install from binaries

| Platform
| ------------------------
| [Linux (x64)][linux]
| [macOS (x64)][darwin]
| [Windows (x64)][windows]

```sh
# For linux/mac
chmod +x kpt

./kpt version
```

### Install from source

```sh
GO111MODULE=on go get -v github.com/GoogleContainerTools/kpt
```

### [Documentation][docs]

See the [docs] for more information on how to use `kpt`.

---

[linux]: https://storage.googleapis.com/kpt-dev/latest/linux_amd64/kpt
[darwin]: https://storage.googleapis.com/kpt-dev/latest/darwin_amd64/kpt
[windows]: https://storage.googleapis.com/kpt-dev/latest/windows_amd64/kpt.exe
[docs]: https://googlecontainertools.github.io/kpt
