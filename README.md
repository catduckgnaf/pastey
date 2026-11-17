# pastey

**Forked from [Cesura/pastey](https://github.com/Cesura/pastey)**

A lightweight, self-hosted paste platform.

## Why this fork

This fork preserves catduck's Pastey build. The former `arcscloud/pastey` image disappeared from Docker Hub, so the source and image are now maintained here.

Compared with upstream, this build:

- Removes TensorFlow and `guesslang` to keep the image lighter.
- Supports a configurable default paste expiry with an expiry picker.
- Supports IPv4 and IPv6 whitelist networks using `ip_network`.
- Defaults to the Dark theme while retaining the theme assets.

The upstream BSD-3-Clause license is retained in [`LICENSE`](LICENSE), and upstream credit is preserved above.

## Features

- Self-contained system without external database dependencies
- Optional on-disk encryption
- Optional single-use pastes
- Optional expiration date
- QR code generation
- IP/network whitelisting and blocking
- Endpoint rate limiting
- JSON API
- Configurable via environment variables

## Docker

```sh
docker run -d --name pastey -p 5000:5000 \
  -v /path/to/local/dir:/app/data \
  ghcr.io/catduckgnaf/pastey:latest
```

Pastey will be accessible at <http://localhost:5000>. Set `PASTEY_DEFAULT_THEME=Dark` to explicitly select the Dark theme. Persistent paste storage is mounted at `/app/data`.

## Local installation

Requirements: Python 3.8 or newer.

```sh
git clone https://github.com/catduckgnaf/pastey.git
cd pastey
mkdir -p data
pip install -r requirements.txt
python app.py
```

## Configuration

| Environment variable | Description | Default |
| --- | --- | --- |
| `PASTEY_DATA_DIRECTORY` | Local directory for paste storage | `./data` |
| `PASTEY_LISTEN_ADDRESS` | Address to listen on | `0.0.0.0` |
| `PASTEY_LISTEN_PORT` | Port to listen on | `5000` |
| `PASTEY_DEFAULT_THEME` | Default theme (`Dark` or `Light`) | `Dark` |
| `PASTEY_DEFAULT_PASTE_EXPIRY` | Default paste expiry in hours; `0` means no expiry | `6` |

Other upstream configuration options remain available; see [`pastey/config.py`](pastey/config.py) for defaults.
