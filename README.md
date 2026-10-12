# Sparky AD Server

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23309050.svg)](https://doi.org/10.5281/zenodo.23309050)

This repository provides a post-installation script to configure a Samba Active Directory (AD) Domain Controller (DC) on SparkyLinux and other Debian-based systems. The script automates the setup process, including dependency installation, network configuration, and Samba provisioning.

## Features

-   **Automated Setup**: A dialog-based installer that guides you through the entire setup process.
-   **Samba AD DC**: Configures a fully functional Samba AD DC.
-   **Network Configuration**: Supports single and bonded network interfaces with static IP configuration.
-   **Automated Backups**: Includes a script for daily backups of your Samba provision.
-   **Optional Components**: Allows for the optional installation of:
    -   ClamAV for antivirus protection.
    -   NUT for UPS support.
    -   Netdata for real-time monitoring.
    -   Webmin for a web-based administration interface.

## Dependencies

The installer script requires the following packages:

-   `apt`
-   `bash`
-   `coreutils`
-   `dialog`
-   `dpkg`
-   `gawk`
-   `grep`
-   `hostname`
-   `iputils-ping`
-   `nano`
-   `sed`
-   `sparky-ntp-server`
-   `sudo`

The `sparky-ad-server` script will install additional dependencies as needed, including the Samba packages and any optional components you select.

## Installation

1.  Clone this repository to your local machine:
    ```bash
    git clone <repository-url>
    ```

2.  Navigate to the cloned directory:
    ```bash
    cd sparky-ad-server
    ```

3.  Run the installation script with root privileges:
    ```bash
    sudo ./install.sh
    ```
    This will copy the necessary files to `/usr/bin` and `/usr/share/sparky/sparky-ad-server`.

## Usage

After installation, you can run the main setup script with root privileges:

```bash
sudo sparky-ad-server
```

The script will guide you through a series of dialogs to configure your Samba AD server. A log file will be created at `/var/log/sparky-ad-server.log`.

## Backups

This repository includes a backup script, `sparky-ad-sambabkp`, which is automatically installed as a weekly cron job. The script will back up your Samba provision, including the `sysvol`, `private`, and configuration files.

By default, backups are stored in a directory found by `find /home/ -iname samba_backup` and are retained for 90 days. You can customize these settings by running the script manually:

```bash
sudo sparky-ad-sambabkp [provisiondir] [destinationdir] [retpd]
```

-   `provisiondir`: The directory of your Samba provision.
-   `destinationdir`: The directory to store the backup archives.
-   `retpd`: The retention period in days.

## Uninstallation

To uninstall Sparky AD Server, run the `install.sh` script with the `uninstall` argument:

```bash
sudo ./install.sh uninstall
```

This will remove the files that were copied during installation. Note that this will not undo the changes made by the `sparky-ad-server` script.

## Troubleshooting

-   **Log File**: The first place to look for errors is the log file at `/var/log/sparky-ad-server.log`.
-   **Network Issues**: Ensure that you have a stable network connection and that your DNS settings are correct.
-   **Permissions**: The scripts must be run with root privileges.

## License

This program is free software and is distributed under the terms of the GNU General Public License, version 3 or later. See the `LICENSE` file for more details.
