Elasticsearch 重要設定
========

## 設定

`/etc/elasticsearch/elasticsearch.yml`

```
cluster.name: cluster_name

node.name: node_name

path.data: /path/to/data/1,/path/to/data/2

bootstrap.mlockall: true

discovery.zen.minimum_master_nodes: floor(n+1)/2

discovery.zen.ping.multicast.enabled: false
```

`/etc/default/elasticsearch`

```
ES_HEAP_SIZE = 2G
MAX_LOCKED_MEMORY = unlimited
MAX_MAP_COUNT = 262144
```

## Tips


1.避免 over-sharding

2.以時間切 index

3.了解資料的 mapping

4.善用 index template

5.定期 optimize index

6.善用 Curator + crontab

7.避免過大的 mapping

