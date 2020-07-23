ELK
===

Docker-compose :
- Elasticsearch:7
- Logstash:7
- Kibana:7


## Install

1. Pull images

```
docker-compose pull
```

2.1. Prepare **elasticsearch** volume

```
mkdir -p elasticsearchi/data elasticsearch/backups
sudo chown -R 1000:1000 Elasticsearch
```

> If an error occur during elasticsearch startup redo the last commands

2.2. Elasticsearch requirements

Elastcsearch need a limit on mmap counts equal to 262144 or more.  
Use script named `set_max_map_count.sh`, required superuser (sudo).

```
./set_max_map_count.sh
```

3. Start dockers

```
docker-compose up -d elasticsearch kibana
```

4. (optional) Logs

```
docker-compose logs -f
```

## X-pack

X-pack is disabled in config files.  
To enable it change 
```
xpack.security.enabled: false
```
to
```
xpack.security.enabled: true
```
in
- **config/kibana.yml**
- **config/elasticsearch.yml**

To create default users:

```
docker-compose up -d elasticsearch
docker-compose exec elasticsearch bin/elasticsearch-setup-passwords auto
```


