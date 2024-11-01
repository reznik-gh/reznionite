# reznionite &nbsp; [![build-ublue](https://github.com/reznik-gh/reznionite/actions/workflows/build.yml/badge.svg)](https://github.com/reznik-gh/reznionite/actions/workflows/build.yml)

## Allgemeines
 Mein eigenes ublue image. Gebaut nach der Anleitung auf [BlueBuild docs](https://blue-build.org/how-to/setup/).
 ![Screenshot  der KDE Konsole mit den Ausgaben von 'rpm-ostree status' und 'fastfetch'](/reznionite-screenshot.png)
 
 ### Basiert auf
 kinoite-nvidia
 
 ### Hinzugefügte Pakete
 - fastfetch & fastfetch-bash-completion
 - steam-devices
 - yt-dlp &  yt-dlp-bash-completion
 - pwgen
 - screen
 - xorg-x11-nvidia
 
 ### Entfernte Pakete
 - firefox &  firefox-langpacks
 - just
 
 ### Hinzugefügte Dateien
 *noch nichts*
 
 ### Hinzugefügte configs
 *noch nichts*


## Installation

> [!WARNING]
> [Das hier ist ein experimentells Feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable). *Eltern haften für ihre Kinder.*

Für ein rebase von einer existierenden Fedora atomic Installation zum aktuellsten Build:

- Zuerst ein rebase zum unsignierten Image, um die Schlüssel und die policies zu bekommen:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/reznik-gh/reznionite:latest
  ```
- Dann den ganzen Bumms neustarten:
  ```
  systemctl reboot
  ```
- Jetzt noch ein rebase zum signierten Image:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/reznik-gh/reznionite:latest
  ```
- Noch ein reboot:
  ```
  systemctl reboot
  ```

## Verifizierung

Diese Images sind mit [Sigstore](https://www.sigstore.dev/)s [cosign](https://github.com/sigstore/cosign) signiert. Du kannst die Signatur verifizieren, indem du die `cosign.pub` aus diesem Repo runterlädst und folgenden Befehl ausführst:

```bash
cosign verify --key cosign.pub ghcr.io/reznik-gh/reznionite
```
  
## ISO

Es ist möglich eine Iso als Installationsmedium zu generieren, wenn der ganze Bumms direkt auf Fedora Atomic basiert. Kann man aber nicht auf Github hosten, da die ISOs zu groß sind.  Infos wie das geht gibt es [hier](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).
