# docker-arr-suite

Automate media downloads and library management with a Docker Compose stack that connects qBittorrent, Radarr, Sonarr, Prowlarr, and related services. Route download traffic through Gluetun and expose web applications through Traefik with HTTPS support.

## Features

- Route qBittorrent traffic through Gluetun with support for OpenVPN and WireGuard providers.
- Forward the VPN port to qBittorrent so incoming connections can use the provider-assigned port.
- Connect Radarr and Sonarr to Prowlarr for centralized indexer configuration.
- Unpack completed downloads with Unpackerr before media import.
- Provide request interfaces through Overseerr or Jellyseerr and stream libraries with Plex or Jellyfin.
- Keep container images current with Watchtower when enabled in the Compose configuration.

**Review the Compose file before starting the stack.** Set paths, credentials, VPN settings, domains, and every required environment variable for your host.

## Installation

Install Docker Engine with the Compose plugin and Go before building the project. Then clone and build the application:

```sh
git clone https://github.com/pvd-nerd/docker-arr-suite "$HOME/media_stack"
cd "$HOME/media_stack"
go build -o docker-arr-suite .
```

Check the available commands and options:

```sh
./docker-arr-suite --help
```

Prepare the Compose environment described by the project configuration. Update volume paths and uncomment only the services and variables you intend to use. Pull the container images before the first launch:

```sh
sudo docker compose pull
```

## Usage

Run the built application and inspect its command-line help:

```sh
./docker-arr-suite --help
```

Start the configured Docker stack with Compose:

```sh
sudo docker compose up -d
```

Initial startup can take some time. Services with missing environment variables may restart until their configuration is complete. Check their logs while finishing setup:

```sh
sudo docker compose logs -f
```

Configure the applications from their web interfaces after startup. Add Prowlarr indexers, connect Prowlarr to Radarr and Sonarr, configure qBittorrent download paths, and set the media server library paths to match the shared volumes in the Compose file.

## License

This project is licensed under the MIT License. It is based on [pvd-nerd/docker-arr-suite](https://github.com/pvd-nerd/docker-arr-suite), and that project is credited here in accordance with its MIT license.
