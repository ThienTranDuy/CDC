
# Run app
## Start the application
export DEBEZIUM_VERSION=2.1
docker compose -f docker-compose.yaml up --build || docker-compose up

## Start Elastic search connector
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @es-sink.json

## Start MySQL connector
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @source.json

# Monitor
## Watching Kafka
http://localhost:8080/

## Watching Kibana
http://localhost:5601/

## Use command
curl -X GET 'http://localhost:9200/customers/_search?pretty' -H 'Content-Type: application/json' -d'
{
  "query": {
    "match": {
      "email": "foobar.com"
    }
  }
}'


docker compose -f docker-compose-kibana.yaml up