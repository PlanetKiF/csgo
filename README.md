# csgo
Planet KiF CS:GO server configuration.

https://planet-kif.de

![Copy files to CSGO Server](https://github.com/PlanetKiF/csgo/workflows/Copy%20files%20to%20CSGO%20Server/badge.svg)


Alles unterhalb des `csgo` directory Repository wird nach jedem commit automatisch auf den Lifeserver kopiert (~~`csgo` in `/home/ubuntu/csgosv` ~~). Ggf. muss  danach auf dem Server mit `rcon exec` die entsprechende Config neu eingelesen werden bzw. ein `changelevel` gemacht werden.

Im Moment hat der copy-Job noch das Verzeichnis `test` in `/home/ubuntu` zum Ziel.


