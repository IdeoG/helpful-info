# Post-installation Manjaro configuration

## Update system

``` bash
sudo pacman -S yaourt
yaourt -Syy
yaourt -Syu
```

## Development tools

``` bash
yaourt -S arduino
yaourt -S android-studio
yaourt -S unity-editor
yaourt -S code
yaourt -S qt-designer
```

## Printer configuration

``` bash
yaourt -S system-config-printer
```

Open system-config-printer. Connect to CUPS and add new printer
