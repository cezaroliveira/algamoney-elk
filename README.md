# algamoney-elk

# Problem using WSL 2

## Elasticsearch

When starting Elasticsearch on Docker, is showing the problem below:

> [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

> ERROR: Elasticsearch did not exit normally - check the logs at /usr/share/elasticsearch/logs/docker-cluster.log

It occurs because of the variable below:

```bash
cat /proc/sys/vm/max_map_count
```

To solve this, inside of WSL 2 image (Ubuntu, Alpine, Centios, etc), execute the code below:

```bash
sudo sysctl -w vm.max_map_count=262144
```

Check if change occurred:

```bash
cat /proc/sys/vm/max_map_count
```

## Filebeat

When starting Filebeat on Docker, is showing the problem below:

> Exiting: error loading config file: config file ("filebeat.yml") must be owned by the user identifier (uid=0) or root

It occurs because of Beats permission rule, as seen below.

> https://www.elastic.co/guide/en/beats/libbeat/5.3/config-file-permissions.html

To solve this, execute the code below:

```bash
sudo chown root filebeat.yml
```
