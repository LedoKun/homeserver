# Home Media Server Stack

This project sets up a comprehensive home media server stack using Docker Compose. It includes various services for media management, streaming, downloading, and network management.

## Prerequisites

- Docker and Docker Compose installed on your system
- A server or NAS with sufficient storage and processing power
- Basic understanding of Docker and networking concepts

## Setup Instructions

1. Clone this repository to your local machine or server.

2. Create the necessary directories:

   ```bash
   mkdir -p /srv/media/config /srv/media/data
   mkdir -p /srv/media/config/{caddy,prowlarr,sonarr,radarr,qbittorrent,jellyfin,filebrowser,audiobookshelf,readarr,boinc,scrutiny,blocky}
   mkdir -p /srv/media/data/public/{TV,Movies,Anime,Books,Audiobooks,Podcasts}
   ```

3. Copy the `.env.example` file to `.env` and update the variables according to your environment:

   ```bash
   cp .env.example .env
   ```

   Edit the `.env` file and adjust the values as needed.

4. Create the external network for Caddy:

   ```bash
   docker network create caddy-public
   ```

5. Deploy the stack:

   ```bash
   docker-compose up -d
   ```

## Services

The stack includes the following services:

- **Caddy**: Reverse proxy and automatic HTTPS
- **Prowlarr**: Indexer manager
- **Sonarr**: TV show management
- **Radarr**: Movie management
- **qBittorrent**: Torrent client
- **Jellyfin**: Media streaming server
- **FileBrowser**: Web-based file manager
- **Audiobookshelf**: Audiobook and podcast server
- **Readarr**: Book and audiobook management
- **BOINC**: Distributed computing platform
- **Scrutiny**: Hard drive monitoring
- **Blocky**: DNS server with ad-blocking capabilities
- **Watchtower**: Automatic Docker container updates

## Configuration

Most services can be configured through their web interfaces. Default ports and paths are defined in the `docker-compose.yml` file.

### Important Notes

- The Caddy service requires access to a Tailscale network. Make sure Tailscale is properly set up on your server.
- Jellyfin is configured to use hardware acceleration. Ensure your system supports this feature.
- The BOINC service is set to run only on the "ledokun" node. Adjust this constraint if needed.
- Scrutiny is configured to monitor specific drives. Update the devices section in the `docker-compose.yml` file to match your system's drives.

## Networking

The stack uses two networks:

- `caddy-public`: Used by most services for inter-container communication
- `caddy-host`: Used by Caddy to access the host network

## Updating

The Watchtower service is configured to automatically update all containers daily at 4:00 AM. You can also manually update containers using Docker Compose:

```bash
docker-compose pull
docker-compose up -d
```

## Troubleshooting

- If you encounter permission issues, ensure the PUID and PGID in the `.env` file match your user's ID and group ID.
- Check the logs of individual services for more detailed error messages:

  ```bash
  docker-compose logs [service_name]
  ```

## Contributing

Feel free to open issues or submit pull requests if you have suggestions for improvements or encounter any problems.

## License

This project is open-source and available under the MIT License.
