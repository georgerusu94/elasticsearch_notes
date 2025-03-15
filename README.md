#Register repository for snapshot
curl -X PUT "localhost:9200/_snapshot/my_backup_repository" -H 'Content-Type: application/json' -d '{
  "type": "fs",
  "settings": {
    "location": "/mnt/backups/elasticsearch",
    "compress": true
  }
}'

#Create snaphot
curl -X PUT "localhost:9200/_snapshot/my_backup_repository/snapshot_1?wait_for_completion=true"

#Verify snapshot
curl GET "localhost:9200/_snapshot/my_backup_repository/snapshot_1"

#Resotre snapshot
curl -X POST "localhost:9200/_snapshot/my_backup_repository/snapshot_1/_restore



path.repo: "/mnt/backups/elasticsearch"




#Check nodes:
curl -s 'http://localhost:9200/_cat/nodes?v&h=name,version,master' | column -t

#Check shards:
curl 'http://localhost:9200/_cat/shards'

#
curl -X PUT 'http://localhost:9200/_cluster/settings?pretty' -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": "all"
  }
}'

#Flush:
curl -X POST 'http://localhost:9200/_flush/synced?pretty'


#Health:
curl 'http://localhost:9200/_cluster/health?pretty'


#Stop container:
docker stop <container>
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.17.15

docker-compose -f elastic-docker-compose-6.8.23.yml pull elasticsearch-node2
docker-compose -f elastic-docker-compose-6.8.23.yml up -d --no-deps --build elasticsearch-node2

#
curl -X PUT 'http://localhost:9200/_cluster/settings?pretty' -H 'Content-Type: application/json' -d'
{
  "persistent": {
    "cluster.routing.allocation.enable": null
  }
}'

#Snapshot





GET _search
{
  "query": {
    "match_all": {}
  }
}

PUT /my_index
{
  "mappings": {
    "my_type": {
      "properties": {
        "name": {
          "type": "text"
        },
        "age": {
          "type": "integer"
        },
        "email": {
          "type": "keyword"
        }
      }
    }
  }
}

GET /my_index/my_type/_search

POST /my_index/my_type/1
{
  "name": "John Doe",
  "age": 30,
  "email": "johndoe@example.com"
}

POST /my_index/my_type/2
{
  "name": "Jane Smith",
  "age": 25,
  "email": "janesmith@example.com"
}
