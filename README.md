# sergelevin/minidlna

[ReadyMedia](http://minidlna.sourceforge.net/) (formerly MiniDLNA) is server software with the aim of being fully compliant with DLNA/UPnP-AV clients. It is developed by a NETGEAR employee for the ReadyNAS product line. So if you are looking for a NAS, please consider ReadyNAS first! 

## Licensing
You are permitted to use the provided software under the terms contained in LICENSE file.
The resulting image is based on linuxserver.io xenial [base image](https://hub.docker.com/r/lsiobase/xenial/) and contains [ReadyMedia](http://minidlna.sourceforge.net/) as a part. These components might be licensed under their separate license, which could be found on the websites of the corresponding projects.

## Usage

```
docker create \
	--name=minidlna \
	--net=host \
	-e PUID=<UID> -e PGID=<GID> \
	-v </path/to/library>:/config \
	-v <path/to/tvseries>:/data \
	sergelevin/minidlna
```

**Parameters**

* `--net=host` - Shares host networking with container, **required**.
* `-v /config` - miniDLNA library, logs and config file location.
* `-v /data` - Media goes here. Several entries may be added, e.g. `/data/movies`, `/data/tv`, etc.
* `-e PGID=` for for GroupID - see below for explanation
* `-e PUID=` for for UserID - see below for explanation

It is based on [linuxserver.io](https://linuxserver.io) xenial [base image](https://hub.docker.com/r/lsiobase/xenial/) and compatible with user and group id specification supported be them.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" <sup>TM</sup>.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

You can create container running with your own user id and group specifying parameters as below:
```
	-e PUID=`id -u` -e PGID=`id -g`
```
