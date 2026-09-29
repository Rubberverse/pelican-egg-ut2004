# Pelican Egg for UT2004

> [!WARNING]
> By using this egg, you acknowledge and accept Epic Games Terms of Service agreement.

If you do not accept it, don't use this.

## Credits

All resources I've used and modified to suit this egg

- [OldUnreal/FullGameInstallers](https://github.com/OldUnreal/FullGameInstallers/tree/master/Linux) for the Linux installer. There's a modified copy here that skips interactive consent and assumes it was granted by simply agreeing to run the egg, only `setup::eula` CLI section was modified
- [GFXSpeed/ut2004_pterodactly](https://github.com/GFXSpeed/ut2004_pterodactyl) for `setup.sh` and general idea on how to work around Pterodactyl / Pelican eggs
- [Pelican-Eggs/yolks](github.com/pelican-eggs/yolks) maintainers for their brilliant runner & installer Dockerfiles
- [PhasecoreX/docker-ut2004-server](https://github.com/PhasecoreX/docker-ut2004-server) for inspiration

## What is this?

If you're here by chance, this is an egg that's supposed to be used with Pelican Wings. If you don't know what Pelican is, it's a self-hostable game panel where you can spin up new game servers, manage them, give people access to them etc.

It's basically like running your own game hosting at home. A lot of smaller and medium sized hosts use Pterodactyl, or Pelican for their panel so if you ever used those then this interface will feel very familiar to you. Pull requests are enabled now so if you spot an issue you can just do a PR, might have gotten turned off when I was moving repositories to this organization.

## Actual README

I've been dying to play some good arena shooter for a while now. After looking through my search engine of choice - DuckDuckGo - I didn't find anything that *worked* for me. These eggs were outdated, were relying on somebody else hosting the download on Google Drive and others just relied on the very outdated version of UT2004 for their server needs. I was bored out of my mind so I decided to say fuck it, how hard may it be?

Few hours later I was spinning up my own yolks for this, they can be found [in this repository](https://github.com/MrRubberDucky/yolks/tree/main) and writing a whole ass Pelican install script. It's just time consuming if anything.

Here I bring you: UT2004 server egg with all the bells and whistles. It makes use of a modified OldUnreal's project install script which handles installing latest game version and patching it, then makes use of my rather simple Debian Trixie runner image to run on, which is pinned against short SHA256 commit. Server starts, runs, properly reports as Running in the dashboard and well it's just UT2004 server, rest is up to you to change. Maybe in the near future I could patch this check dynamically without needing to literally grab the entire OU install script, editing lines with `sed` is a bit cumbersome though.

I didn't wanna offload thousand of variables for you to change within dashboard so for anything more advanced, dive into `System/UT2004.ini` and modify it to your liking.

## Ports

You can change game and webadmin port to be anything you want. I'll use 7777/udp as my example. Query & GameSpy query get calculated from following formula: `{{GAME_PORT}}+1=Query`, `{{GAME_PORT}}+10=GameSpy_Query`

- 7777/udp - Game
- 7778/udp - Query
- 7787/udp - GameSpy Query
- 9000/tcp - WebAdmin (XAdmin)
- 28902/udp - Connection to Master Server(s), needs to be manually configured in `UT2004.ini`
