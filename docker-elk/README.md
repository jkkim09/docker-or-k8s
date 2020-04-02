클러스터는 여러 노드의 집합으로 구성되며, 설치시 master node만 존재
primary shard는 데이터를 저장할 때 나눠진 파티션을 말하며, 설치시 5개가 존재
replica shard는 고가용성을 위해 존재하는 primary shard의 복제본을 말하며, 설치시 1개가 존재
primary와 replica는 같은 노드에 존재할 수 없음<br><br>

replica는 primary와 같은 노드상에 있을 수 없습니다.
즉, 현재는 하나의 노드가 실행 중이므로 replica를 배정할 수 없게 됩니다.
나중에 다른 노드가 클러스터에 포함되면 replica를 배정할 수 있고, 배정되면 green status로 바뀝니다.

``````sh
curl -XGET localhost:9200/_cat/indices?v
curl -XGET localhost:9200/_cat/shards?v
curl -XPUT 'localhost:9200/_settings?pretty' -d '{"index":{"number_of_replicas": 0}}' -H 'Content-Type: application/json'
``````
