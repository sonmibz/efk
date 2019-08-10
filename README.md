
### Introduction
EFK (elasticsearch+fluentd+kibana) with docker

### Usage
first, build fluentd image that contains elasticsearch plugin.

```bash
docker build --tag fluentd:es fluentd/
```

and then, docker compose up

```bash
docker-compose up
```

### vm.max_map_count for elasticsearch
set maximum number of memory map areas a process may have.

```bash
sysctl -w vm.max_map_count=262144
```

### fluentd.conf (app log server)

```text
<source>
 ~~ setting ~~
</source>

<match changeme>
    @type forward
    send_timeout 60s

    <server>
        name logserver
        host 127.0.0.1
        port 24224
        weight 60
    </server>
</match>
```


