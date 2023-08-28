# dane-download-worker

DANE worker that downloads input files for other DANE workers. Input is provided in the form of a URI. S3 URIs are also supported.

# Installation

## Run locally:

Prerequisites:

- Python 3.10.x
- [Poetry](https://python-poetry.org/)

```sh
poetry install
poetry shell
python ./worker.py
```

## Docker

```sh
docker build -t dane-download-worker .
```

# Configuration

Make sure the create, and fill in to match your environment, the following `config.yml`:

```yaml
RABBITMQ:
    HOST: your-rabbit-mq-host  # set to your rabbitMQ server
    PORT: 5672
    EXCHANGE: DANE-exchange
    RESPONSE_QUEUE: DANE-response-queue
    USER: guest # change this for production mode
    PASSWORD: guest # change this for production mode
ELASTICSEARCH:
    HOST: ["elasticsearch-host"]  # set to your elasticsearch host
    PORT: 9200
    USER: "" # change this for production mode
    PASSWORD: "" # change this for production mode
    SCHEME: http  # OR https
    INDEX: your-dane-index  # change to your liking
LOGGING:
    LEVEL: INFO
PATHS: # common settings for each DANE worker to define input/output dirs (with a common mount point)
    TEMP_FOLDER: "./mount" # directory is automatically created (use ./mount for local testing)
    OUT_FOLDER: "./mount" # directory is automatically created (use ./mount for local testing)
DOWNLOADER:
    FS_THRESHOLD: 10GB # use xxGB, xxTB, etc
    WHITELIST:
        - myownvideos.com # valid domain name
```


# Run

The best way to run is within a Kubernetes environment, together with the following:

- DANE-server
- RabbitMQ server
- Elasticsearch cluster

Documentation on how to setup this environment will be linked later on
