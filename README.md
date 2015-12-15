# Docker ELK Stack

| Lib         | Version | Doc |
|-------------|---------|-----|
| Elastic(search)     | v2.1.0  | [guide](https://www.elastic.co/guide/en/elasticsearch/guide/current/index.html)  |
| Logstash            | v2.1.0  | [guide](https://www.elastic.co/guide/en/logstash/current/index.html)  |
| Kibana              | v4.3.0  | [guide](https://www.elastic.co/guide/en/kibana/current/index.html)  |

Everything you need to run the ELK stack on your logs and build dashboards to:

* Monitor your production environments.
* Help to debug in dev process.
* Build statistics on users behaviors.
* Much more !!!

The image is done to work with Symfony application logs and for Apache and Nginx web servers
but you can easily extends the image and add your own patterns and configurations.

## Container management

```shell
make start
make stop
make remove
make state # Container status
make bash # Log into another elk container instance
make build # Rebuild the image
```
## SSL

Logstash use SSL certificates to secure data transfer. Default certificates are included in the built image.
The default certificate is available in the `ssl` directory.
If you want to generate new SSL certificates for security reasons for instance:

```shell
sudo openssl req -x509 -nodes -newkey rsa:2048 \
    -keyout logstash-forwarder.key -out logstash-forwarder.crt
```

## Logstash filters

You can find them in the `filters` directory.
Add you own and add a volume before starting the container or create your own derived image.

```shell
-v $(pwd)/filters/CUSTOM-FILTER.conf:/etc/logstash/conf.d/CUSTOM-FILTER.conf
```

```shell
ADD ./filters/CUSTOM-FILTER.conf /etc/logstash/conf.d/CUSTOM-FILTER.conf
```

## Logstash patterns

You can find them in the `patterns` directory.
Add you own and add a volume before starting the container or create your own derived image.

```shell
-v $(pwd)/patterns/CUSTOM.pattern:/opt/logstash/patterns/CUSTOM
```

```shell
ADD ./patterns/CUSTOM.pattern ${LOGSTASH_HOME}/patterns/CUSTOM
```

## Elasticsearch configuration

You can find it in the `conf` directory.
Feel free to update it !