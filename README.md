[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/index.php/irc/
[podcasturl]: https://www.linuxserver.io/index.php/category/podcast/

[![linuxserver.io](https://www.linuxserver.io/wp-content/uploads/2015/06/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/sickbeard
[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/sickbeard.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/sickbeard.svg)][hub][![Build Status](http://jenkins.linuxserver.io:8080/buildStatus/icon?job=Dockers/LinuxServer.io-armhf/lsioarmhf-sickbeard)](http://jenkins.linuxserver.io:8080/job/Dockers/job/LinuxServer.io-armhf/job/lsioarmhf-sickbeard/)
[hub]: https://hub.docker.com/r/lsioarmhf/sickbeard/

The ultimate PVR application that searches for and manages your TV shows
Automatically finds new and old episodes for you and it works with your current download client!. Includes updated python ssl for newer sites like PTP etc.[Sickbeard](http://sickbeard.com/)

[![sickbeard](http://wolfeden.ca/sickbeard_small.png)][sickurl]
[sickurl]: http://sickbeard.com/
## Usage

```
docker create --name=sickbeard \
-v <path to data>:/config \
-v <path to downloads>:/downloads \
-v <path to tv-shows>:/tv \
-e PGID=<gid> -e PUID=<uid> \
-e TZ=<timezone> \
-p 8081:8081 \
lsioarmhf/sickbeard
```

**Parameters**

* `-p 8081` - the port(s)
* `-v /config` - where sickbeard should store its config files etc.
* `-v /downloads` - your downloads folder
* `-v /tv` - your tv-shows folder
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it sickbeard /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application 
`IMPORTANT... THIS IS THE ARMHF VERSION`

Web interface is at `<your-ip>:8081` , set paths for downloads, tv-shows to match docker mappings via the webui.


## Info

* To monitor the logs of the container in realtime `docker logs -f sickbeard`.

## Versions

+ **07.09.16:** Initial Release.
