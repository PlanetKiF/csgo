# csgo
Planet KiF CS:GO server configuration.

https://planet-kif.de

![Copy files to CSGO Server](https://github.com/PlanetKiF/csgo/workflows/Copy%20files%20to%20CSGO%20Server/badge.svg)

Alles im Repository (ausser .git* Dateien und Ordnern) wird nach jedem Commit automatisch auf den Lifeserver kopiert (z.B. `csgosv` in `/home/ubuntu/csgosv`). Ggf. muss danach auf dem Server mit `rcon exec` die entsprechende Config neu eingelesen werden bzw. ein `changelevel` gemacht werden.

Ggf. müssen im `bin` Ordner die Ausführungsberechtigungen auf den Skripten gesetzt werden.


