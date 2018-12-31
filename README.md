# scher200/syslog

## About

A very simple `socat` based syslog server designed to listen to syslog on `TCP`, `UDP` or a UNIX syslog `/syslog/sock`| rsyslog `/dev/log` and print any messages to `stdout` so that they get picked up by the docker log system and can be accessed via tools like [logspout](http://github.com/gliderlabs/logspout).

## Usage

```
$ docker run -d scher200/syslog [-t tcp|udp|socket]
```

## Examples

Listen on TCP 5140 on host:

```
$ docker run -d -p 5140:514 scher200/syslog -t tcp
```

Listen on UDP 5140 on host:

```
$ docker run -d -p 5140:514/udp scher200/syslog -t udp
```

Listen on a socket which is volume mounted into another container:

```
$ docker run -d --name syslog -v /syslog/socket scher200/syslog -t rsyslog
$ docker run -ti  --volumes-from syslog defensative/socat-ubuntu UNIX:/syslog/socket -
test
test
test
CTRL^C
$ docker logs syslog
==> syslog listening on socket
test
test
test
```
