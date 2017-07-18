e3k-docker
==========

**E**lasticsearch / **E**lasticsearch-head / **E**mbulk / **K**ibana

## Requirements

- Docker
- docker-compose

## Quick start

`docker-compose up -d`

- elasticsearch-head: `http://localhost:9100`
- kibana: `http://localhost:5601`

## Versions

- edit `./.env`

```
# elasticsearch
ELASTICSEARCH_VERSION=5.5.0

## plugin: kuromoji-neologd
KUROMOJI_NEOLOGD_VERSION=5.2.1

# embulk
EMBULK_VERSION=0.8.26

# kibana
KIBANA_VERSION=5.5.0
```

## Plugins

### Elasticsearch

- edit `./elasticsearch/Dockerfile`
- preset
    - analysis-icu
    - analysis-kuromoji
    - analysis-kuromoji-neologd

### Embulk

- edit `./embulk/Dockerfile`
- preset
    - embulk-output-elasticsearch
    - embulk-input-mysql
    - embulk-filter-reverse_geocoding

## Import data with Embulk

Import data directory: `./embulk/import` (mapping to `/import` in embulk container)

### Example

- Import sample csv file

```sh
docker-compose run --rm embulk guess /import/sample_seed.yml -o /import/sample_config.yml
docker-compose run --rm embulk run /import/sample_config.yml
```