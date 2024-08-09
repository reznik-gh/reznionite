# reznionite &nbsp; [![build-ublue](https://github.com/reznik-gh/reznionite/actions/workflows/build.yml/badge.svg)](https://github.com/reznik-gh/reznionite/actions/workflows/build.yml)

Für eine Schnellanleitung zum Aufbau eines eigenen Repository basierend auf diesem hier, rufe [BlueBuild docs](https://blue-build.org/how-to/setup/) auf.

Nach dem Setup solltest du diese README aktualisieren, um dein persönliches Image zu beschreiben. *Yo, sollte ich wohl mal machen, was?* ;)

## Installation

> **Warning**  
> [Das hier ist ein experimentells Feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), Eltern haften für ihre Kinder.

Für ein rebase von einer existierenden Fedora atomic Installation zum aktuellsten Build:
*Wieso sollte man zu etwas anderem als dem aktuellsten wollen? Was für eine unnütze Information. Tsss...*

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
- Noch ein reboot: *Sind wir bald da, Papa Schlumpf?*
  ```
  systemctl reboot
  ```

Der `latest` tag zeigt automatisch auf den neuesten build. *Echt? Kein Scheiß?* Dieser build wird immer die Fedora Version, die in der `recipe.yml` angegeben ist, verwenden, so dass du nicht aus versehen auf die nächste Major Version upgradest. *Und wenn ich lastest in der recipe.yml angeben? Finden wir mit Fedora 41 raus. Learning by doing nennt man das.*

## ISO

Es ist möglich eine Iso als Installationsmedium zu generieren, wenn der ganze Bumms direkt auf Fedora Atomic basiert. *Das ist hier nicht der Fall. Ich lass vorerst hier trotzdem drin, weil es gut zu wissen ist.* Kann man aber nicht auf Github hosten, da die ISOs zu groß sind.  Infos wie das geht gibt es [hier](https://blue-build.org/learn/universal-blue/#fresh-install-from-an-iso).

## Verifizierung

Diese Images sind mit [Sigstore](https://www.sigstore.dev/)s [cosign](https://github.com/sigstore/cosign) signiert. Du kannst die Signatur verifizieren, indem du die `cosign.pub` aus diesem Repo runterlädst und folgenden Befehl ausführst:

```bash
cosign verify --key cosign.pub ghcr.io/reznik-gh/reznionite
```
