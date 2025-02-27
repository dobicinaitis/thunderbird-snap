# Thunderbird Snap

A fork of the [Thunderbird Snap](https://github.com/ubuntu/thunderbird)
that fixes an [issue](https://github.com/balbusm/xul-ext-eds-calendar/issues/68) preventing the
[EDS Calendar Integration](https://addons.thunderbird.net/en-US/thunderbird/addon/eds-calendar-integration) extension
from working in the Snap package.

## Switching to the fork

### Prerequisites

- [snapcraft](https://snapcraft.io/docs/create-a-new-snap#p-36254-h-1-snapcraft-setup)

### Build

Build the custom Snap package using the following command:

```bash
snapcraft
```

This will take a while ... ☕️

### Prepare for the switch

Backup data of the official Thunderbird Snap:

```bash
mkdir ~/Downloads/thunderbird-snap-backup
cp -R ~/snap/thunderbird/* ~/Downloads/thunderbird-snap-backup/
```

Uninstall the official Snap:

```bash
snap remove thunderbird
```

Restore/pre-populate the Snap's `common` directory from the backup:

```bash
mkdir ~/snap/thunderbird
cp -R ~/Downloads/thunderbird-snap-backup/common ~/snap/thunderbird/
```

### Install

Install the freshly built Snap:

```bash
snap install ./thunderbird_*.snap --dangerous
```

Connect the `calendar-service` interface to enable communication between the Snap and Evolution Data Server:

```bash
sudo snap connect thunderbird:calendar-service
```

Open Thunderbird and rejoice! 🎉