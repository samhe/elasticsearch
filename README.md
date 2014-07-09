## ElasticSearch Dockerfile


This repository contains **Dockerfile** of [ElasticSearch](http://www.elasticsearch.org/) for [Docker](https://www.docker.io/)'s [trusted build](https://index.docker.io/u/dockerfile/elasticsearch/) published to the public [Docker Registry](https://index.docker.io/).


### Dependencies

* [dockerfile/java](http://dockerfile.github.io/#/java)


### Installation

1. Install [Docker](https://www.docker.io/).

2. Download [trusted build](https://index.docker.io/u/dockerfile/elasticsearch/) from public [Docker Registry](https://index.docker.io/): `docker pull dockerfile/elasticsearch`

   (alternatively, you can build an image from Dockerfile: `docker build -t="dockerfile/elasticsearch" github.com/dockerfile/elasticsearch`)


### Usage

    docker run -d -p 9200:9200 -p 9300:9300 dockerfile/elasticsearch

#### Attach persistent/shared directories

  1. Create a mountable data directory `<workdir>` on the host.

   ```
   ├── conf
   │   └── elasticsearch.yml
   ├── data
   │   └── hesa2-esh
   ├── logs
   ├── plugins
   │   ├── bigdesk
   │   ├── eseditor
   │   └── head
   └── work
   ```

  2. Create ElasticSearch config file at `<workdir>/elasticsearch.yml`.

    ```yml
    path:
      logs: /workdir/log
      data: /workdir/data
      work: /workdir/work
      plugins: /workdir/plugins
    ```

  3. Start a container by mounting data directory and specifying the custom configuration file:

    ```sh
    docker run -d -p 9200:9200 -p 9300:9300 -v <workdir>:/data dockerfile/elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/workdir/conf/elasticsearch.yml
    ```



After few seconds, open `http://<host>:9200` to see the result.
