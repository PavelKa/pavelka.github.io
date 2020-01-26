## Run ELK, Kibana and Grafana in docker


### install  
```console
docker network create somenetwork
docker run -d --name elasticsearch --net somenetwork -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.4.2
docker run -d --name=grafana -p 3000:3000 grafana/grafana
docker run -d --name kibana --net somenetwork -p 5601:5601 kibana:7.4.2
```

