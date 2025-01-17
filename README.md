influxdb-collectd-proxy
=======================

A very simple proxy between collectd and influxdb.

## Build

Clone this project and just make it.

```
$ make
```

## Usage

First, add following lines to collectd.conf then restart the collectd daemon.

```
LoadPlugin network

<Plugin network>
  # influxdb collectd proxy address
  Server "127.0.0.1" "8096"
</Plugin>
```

And start the proxy.

```
$ bin/influxdb-collectd-proxy --typesdb="/usr/share/collectd/types.db" --database="collectd" --username="collectd" --password="collectd"
```

## Options

```
$ bin/influxdb-collectd-proxy --help
Usage of bin/influxdb-collectd-proxy:
  -database="": database for influxdb
  -hostname-as-column=false: true if you want the hostname as column, not in series name
  -pluginname-as-column=false: true if you want the pluginname as column
  -influxdb="localhost:8086": host:port for influxdb
  -logfile="proxy.log": path to log file
  -normalize=true: true if you need to normalize data for COUNTER types (over time)
  -storerates=true: true if you need to derive rates from DERIVE types
  -password="root": password for influxdb
  -proxyhost="0.0.0.0": host for proxy
  -proxyport="8096": port for proxy
  -typesdb="types.db": path to Collectd's types.db
  -username="root": username for influxdb
  -verbose=false: true if you need to trace the requests
```

## Systemd Unit File

Only tested on Arch Linux. You may have to adjust the path of typesdb for your distro.

```
[Unit]
Description=Proxy that forwards collectd data to influxdb

[Service]
Type=simple
ExecStart=/usr/local/bin/influxdb-collectd-proxy --database=collectd --username=root --password=root --typesdb=/usr/share/collectd/types.db
User=collectd-proxy
Group=collectd-proxy

[Install]
RequiredBy=collectd.service
```

## Dependencies

- http://github.com/paulhammond/gocollectd
- http://github.com/influxdata/influxdb1-client

## References

- http://github.com/bpaquet/collectd-influxdb-proxy

## Contributors

This project is maintained with following contributors' supports.

- porjo (http://github.com/porjo)
- feraudet (http://github.com/feraudet)
- falzm (http://github.com/falzm)
- vbatoufflet (http://github.com/vbatoufflet)
- cstorey (http://github.com/cstorey)
- jeroenbo (http://github.com/jeroenbo)
- yanfali (http://github.com/yanfali)
- linyanzhong (http://github.com/linyanzhong)
- rplessl (http://github.com/rplessl)
