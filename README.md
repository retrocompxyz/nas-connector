# NasConnector

A macOS menu bar app for automatically mounting SMB network shares.
Add your shares once — NasConnector mounts them for you, including at login.

## Downloads

Get the latest version from the [Releases page](https://github.com/retrocompxyz/nas-connector/releases/latest):

- **`NasConnector-<version>-universal.dmg`** — for Apple Silicon **and** Intel Macs.
- **`NasConnector-<version>-arm64.dmg`** — Apple Silicon only (smaller download).

## Requirements

- macOS 13 (Ventura) or newer.
- The **universal** build runs on both Apple Silicon and Intel.
- The **arm64** build runs on Apple Silicon only.

## Installation

1. Download the DMG of your choice.
2. Open the image and drag `NasConnector.app` into the `/Applications` folder.
3. Launch it — an icon will appear in the menu bar.

> **First launch / Gatekeeper.** The app is not notarized by Apple, so macOS may
> block it with a warning. Either right-click the app and choose **Open**, or run:
>
> ```sh
> xattr -dr com.apple.quarantine "/Applications/NasConnector.app"
> ```

## Features

- Mount and unmount SMB shares from the menu bar.
- Manage the share list: add, edit, delete.
- Passwords stored securely in the macOS Keychain.
- Automatically mounts **all** saved shares at login and after the network
  connection is restored.
- Test the connection and credentials before saving a share.
- Support for multiple shares from the same server/IP.

## Usage

Click the menu bar icon to:

- see the share list (click a share to mount/unmount),
- **Add share…**, **Manage shares…**, **Settings…**,
- **Mount all** / **Unmount all**,
- **Launch at login**.

### Share address format

Accepted formats include:

- `//192.168.1.10/share`
- `\\192.168.1.10\share`
- `smb://192.168.1.10/share`
- `192.168.1.10/share`
- `nas.local:4450/data`
- `[fe80::1]:445/share`

### Where shares are mounted

- Shares **with a username and password** are mounted via `/sbin/mount_smbfs`
  into `~/Mounts/<share>`.
- **Guest** shares (empty username) are mounted anonymously via NetFS into
  `/Volumes/<share>`.

> Note: macOS does not allow a regular user to create mount points in `/Volumes`,
> so shares with credentials go to `~/Mounts` (they do not appear as separate
> drives in the Finder sidebar).

## Automatic mounting at login

The app can start with the system (the **Launch at login** option, implemented
via a LaunchAgent). After launch it automatically tries to mount **all saved
shares**, and retries after the network connection is restored.

## Data and logs

- Share list: `~/Library/Application Support/NasConnector/shares.json`
- Passwords: macOS Keychain (service `com.nasconnector.app`)
- Log: `~/Library/Logs/NasConnector/nasconnector.log`

## Author

**RetroComp** — [www.retrocomp.xyz](https://retrocomp.xyz)

## License

Licensed under the **PolyForm Noncommercial License 1.0.0** — free to use for
noncommercial purposes. Commercial use and selling are not permitted; the author
retains all commercial rights. See [LICENSE](LICENSE) for the full text.
