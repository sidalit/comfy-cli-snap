# Comfy CLI snap

[![comfy-cli](https://snapcraft.io/comfy-cli/badge.svg)](https://snapcraft.io/comfy-cli)

Snap packaging for [Comfy CLI](https://github.com/Comfy-Org/comfy-cli), a command-line client for ComfyUI workflows and Comfy Cloud.

Unofficial build, not affiliated with or endorsed by the Comfy project.

## Build

```bash
snapcraft pack
```

## Install and try

<a href="https://snapcraft.io/comfy-cli"><img alt="Get it from the Snap Store" src="https://snapcraft.io/en/dark/install.svg" width="180"></a>

```bash
sudo snap install comfy-cli
comfy-cli --help
sudo snap alias comfy-cli comfy   # optional: upstream command name
```

To use the running `comfyui` server snap:

```bash
sudo snap connect comfy-cli:server comfyui:server
comfy-cli nodes ls --where local
comfy-cli run --workflow workflow.json --where local --wait
```

The connection supplies the server's configured address and port. The CLI does not start or stop the server. Use **Manager → Model Manager** in ComfyUI to install models on the server.

For another server or Comfy Cloud:

```bash
COMFY_LOCAL_URL=http://192.168.1.20:8188 comfy-cli nodes ls --where local
comfy-cli cloud login
comfy-cli jobs ls --where cloud
```

Explicit `--host` and `--port` options override the connection URL. Cloud sign-in keeps upstream's automatic cloud routing; use `--where local` to target your local server.

Configuration and sign-in data live under `~/snap/comfy-cli/common/.config/comfy-cli`.

```bash
sudo snap connect comfy-cli:removable-media   # optional: /media, /mnt
```

## Known limitations

- Local environment installation and management are not supported. Manage the `comfyui` server with snap commands; update this CLI with `sudo snap refresh comfy-cli`.
- CLI model downloads do not install models into the separate server snap.
- Local server URLs use HTTP; HTTPS is not supported by upstream's `COMFY_LOCAL_URL` setting.
- Hidden files in your normal home and arbitrary host programs are unavailable under strict confinement.

## Update to a new upstream release

Change `version` in `snap/snapcraft.yaml`, then rebuild.

## Automation

Builds, publishing, and dependency updates use [snap-automation](https://github.com/sidalit/snap-automation).

## License

The packaging is MIT-licensed (see `LICENSE`). Comfy CLI is GPL-3.0-only-licensed; its dependencies carry their own licenses.
