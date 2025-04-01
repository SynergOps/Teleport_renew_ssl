# Teleport SSL Renewal Script

This repository contains a Bash script to automate the renewal of SSL certificates for [Teleport](https://goteleport.com/), a secure access platform. The script is designed for servers using **systemd** for service management and **Let's Encrypt** for SSL certificates.

## Features

- Automatically stops the Teleport service.
- Renews SSL certificates using `certbot`.
- Configures Teleport with the new certificates.
- Restarts the Teleport service and verifies its status.

## Prerequisites

Before using this script, ensure the following:

1. **Root Privileges**: The script must be run as `root` or with `sudo`.
2. **Certbot Installed**: Install `certbot` for SSL certificate management.
3. **Teleport Installed**: Ensure Teleport is installed and accessible via the `teleport` command.
4. **Systemd Available**: The server must use `systemd` for service management.
5. **Valid Subdomain**: The Teleport service must be configured with a valid subdomain.

## Usage

1. Clone this repository or copy the script to your server.
2. Make the script executable:
    ```bash
    chmod +x teleport_ssl_renew
    ```
3. Run the script with the subdomain as an argument:
    ```bash
    sudo ./teleport_ssl_renew <subdomain>
    ```
    Example:
    ```bash
    sudo ./teleport_ssl_renew example.yourdomain.com
    ```

## Script Workflow

1. **Validation**:
    - Checks if the script is run as root.
    - Verifies the presence of required tools (`certbot`, `teleport`, `systemctl`).
    - Validates the provided subdomain.

2. **SSL Renewal**:
    - Uses `certbot` to renew the SSL certificate for the subdomain.

3. **Teleport Configuration**:
    - Stops the Teleport service.
    - Cleans up old configuration files.
    - Copies the new SSL certificates to the appropriate location.
    - Configures Teleport with the new certificates.

4. **Service Restart**:
    - Restarts the Teleport service.
    - Verifies that the service is running and reachable.

## Troubleshooting

- If the script fails, check the logs for more details:
  ```bash
  journalctl -u teleport -e
  ```
- Ensure the subdomain is reachable and properly configured in DNS.

## Disclaimer

This script is provided as-is. Use it at your own risk. Always test in a staging environment before deploying to production.

## License

This project is licensed under the [MIT License](LICENSE).
