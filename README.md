# csgo
## Planet KiF CS:GO server configuration.

This is the project used to configure the Planet KiF _Counter Strike:Global Offensive_ server. See https://planet-kif.de for more details, in particular how to set up a server in AWS and how to manage it.

This project covers the "userspace" of such a server, in particular the configuration and customization of CS.

Everything that gets modified within the repository will be copied to the server automatically, so there is no need in working with the files on the server itself. A Github action takes care of the copy job. See file `.github/workflows/deploy.yml`

![Copy files to CSGO Server](https://github.com/PlanetKiF/csgo/workflows/Copy%20files%20to%20CSGO%20Server/badge.svg)

## How to use that for your own server

Quite simple:

  1. install a Linux distribution on your machine. We prefer a Debian based environment, therefore some of the scripts/config's/docs might be depending on this. You can use an AWS instance for this, but this repository is independent of that and you may use an old school hosting server as well. You will need SSH access.
  2. install `steamcmd` using your distros package manager. See [docs/setup](https://planet-kif.de/documentation/2021/01/05/setting-up-the-server.html)
  3. install CSGO using `steamcmd` _into a folder called `csgosv` in the homedirectory of a user_, e.g. `home/ubuntu/csgosv` <br>
  **_Not_** into `/usr/local/...` or some other shared folder.<br> See [docs/setup](https://planet-kif.de/documentation/2021/01/05/setting-up-the-server.html)
  4. fork the project
  5. add the list of _secrets_ given below to your new Github project (or organization if that fits)
  6. execute the Github action, either by pushing anything to your new repo or by starting it in the Github UI. If everything went well, then you will find some scripts in a `bin` directory and a few config files were created/modified.
  7. To make the CSGO server start automatically and to try an update every night add the following lines to the users crontab. To do so log in and type `crontab -e`. Validate this using `crontab -l`
  ```
  @reboot /home/ubuntu/bin/csctrl start
  30 5 * * * /home/ubuntu/bin/csctrl upgrade
  ```

If you restart the instance now (`sudo shutdown -r now`), then the server should start the CSGO server during its startup.


## Needed secrets
  * `CSGO_HOST` <br>
     The hostname (or ip (not encouraged)) of your instance, e.g. `cs.planet-kif.de`
  * `CSGO_KEY` <br>
     The SSH private key used to connect to the server. The copy action will use this for a `rsync`, for example. You will need to add the corresponding public key to the Linux machine user running the CS server.
  * `CSGO_USERNAME` <br>
     The username of the user, where you installed the CSGO server to. For example `ubuntu` with its home directory in `/home/ubuntu`
  * `RCON_PASSWORD` <br>
     The CS server will use this RCON password for remote administration using the in-game console.
  * `SERVER_PASSWORD` <br>
     Clients/players that want to connect to the CSGO server will need this password to connect.~~
  * ~~`SLACK_INFORMER_WEBHOOK`~~ <br>
     ~~This webhook will be used to inform a Slack channel of update problems.~~
  * ~~`SLACK_WEBHOOK_URL`~~ <br>
     ~~This webhook will be used by the Github deployment action to inform a Slack channel of the job's result.~~
 *  `NOTIFICATION_WEBHOOK`
    This webhook will be used by the Github deployment action to inform a Discord channel of the job's result.
  * `STEAM_ACCOUNT` <br>
     The steam account the CSGO server is associated to.
  * `STEAM_WEBAPI_AUTHKEY` <br>
     To be able to use Steam Workshop maps you will need to provide a WebAPI key. See  [docs/workshop](https://planet-kif.de/documentation/2021/01/20/workshop.html)
  * `STEAM_WORKSHOP_COLLECTION_ID` <br>
     The server will use the map collection on the Steam Workshop defined by this id. See [docs/workshop](https://planet-kif.de/documentation/2021/01/20/workshop.html)

You may use Slack instead of Discord to receive all the notifications in a channel. Simply provide the secrets/webhooks above and de-uncomment the Slack paragraph in the Github Action definition ('.github/workflows/deploy.yml`).
