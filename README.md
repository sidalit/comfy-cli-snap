<div align="center">

<img src="snap/gui/comfy-cli.png" alt="Comfy CLI logo" width="128" />

# Comfy CLI

**Run ComfyUI workflows and manage jobs from your terminal.**

[![comfy-cli](https://snapcraft.io/comfy-cli/badge.svg)](https://snapcraft.io/comfy-cli)
[![Base: core26](https://img.shields.io/badge/Base-core26-2C8C3C?logo=canonical&logoColor=white)](https://snapcraft.io/core26)
![Confinement: strict](https://img.shields.io/badge/Confinement-strict-2C8C3C)
[![Maintainer: sidaliteir](https://img.shields.io/badge/Maintainer-sidaliteir-2C8C3C?logo=snapcraft&logoColor=white)](https://snapcraft.io/publisher/sidaliteir)
![Architectures: amd64 and arm64](https://img.shields.io/badge/Architectures-amd64%20%7C%20arm64-2C8C3C?logo=linux&logoColor=white)

[Getting Started](#getting-started) · [Configure](#configure) · [Limitations](#limitations) · [Build](#build) · [Support](#support) · [License](#license)

Unofficial snap packaging for [Comfy CLI](https://github.com/Comfy-Org/comfy-cli), a command-line client for local ComfyUI servers and Comfy Cloud.

</div>

---

## Getting Started

<a href="https://snapcraft.io/comfy-cli"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install comfy-cli
comfy-cli --help
```

Connect to an installed, running [`comfyui` server](https://github.com/sidalit/comfyui-snap):

```bash
sudo snap connect comfy-cli:server comfyui:server
comfy-cli nodes ls --where local
comfy-cli run --workflow workflow.json --where local --wait
```

## Configure

This snap has no `snap set` options. Use environment variables to select a server or destination:

| Variable | Accepted values | Default |
| --- | --- | --- |
| `COMFY_LOCAL_URL` | An HTTP server address, such as `http://192.168.1.20:8188`. | Connected server URL; otherwise upstream preferences or `127.0.0.1:8188`. |
| `COMFY_WHERE` | `local`, `cloud` | Project or saved preference; otherwise cloud when credentials are configured, or local. |

```bash
COMFY_LOCAL_URL=http://192.168.1.20:8188 comfy-cli nodes ls --where local
comfy-cli cloud login
comfy-cli jobs ls --where cloud
```

Explicit `--host`, `--port` and `--where` options override the corresponding environment settings. Configuration and sign-in data live in `~/snap/comfy-cli/common/.config/comfy-cli`.

Optional setup:

```bash
sudo snap alias comfy-cli comfy                # upstream command name
sudo snap connect comfy-cli:removable-media    # /media, /mnt
```

## Limitations

- Local environment installation and server startup are not supported. Manage the server through its snap commands.
- CLI model downloads do not install into the server snap. Use **Manager → Model Manager** in ComfyUI.
- `COMFY_LOCAL_URL` supports HTTP, not HTTPS.
- Hidden files directly under your home directory and arbitrary host programs are unavailable.
- Update the CLI with `sudo snap refresh comfy-cli`; its self-updater cannot replace the installed snap.

## Build

```bash
git clone https://github.com/sidalit/comfy-cli-snap.git
cd comfy-cli-snap
sudo snap install snapcraft --classic
snapcraft pack
```

## Support

- **Installation or snap issues:** [open a packaging issue](https://github.com/sidalit/comfy-cli-snap/issues).
- **Application bugs:** [report them upstream](https://github.com/Comfy-Org/comfy-cli/issues).

## License

Snap packaging: [MIT](https://github.com/sidalit/comfy-cli-snap/blob/main/LICENSE).
