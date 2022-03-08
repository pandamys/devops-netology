# Задание 1
Содержимое файла Dockerfile
```
FROM centos:7
ENV container docker
ENV ES_JAVA_HOME /opt/jdk-17
ENV ES_USER elasticsearch
ENV ES_GROUP elasticsearch
ENV ES_HOME /opt/elasticsearch
ENV ES_VOL /var/lib/elasticsearch
ENV ES_VERSION 8.0.1

COPY elasticsearch.yml /usr/share/elasticsearch-${ES_VERSION}/config/elasticsearch.yml
COPY elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz /usr/share/elasticsearch
COPY elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz.sha512 /usr/share/elasticsearch
COPY openjdk-17_linux-x64_bin.tar.gz /usr/share/elasticsearch
WORKDIR /usr/share/elasticsearch
RUN yum -y install wget tar perl-Digest-SHA shasum; \
    tar xvf openjdk-17_linux-x64_bin.tar.gz; \
    mv jdk-17 /opt/; \
    mkdir /var/log/elasticsearch /var/lib/elasticsearch /etc/default/elasticsearch /etc/elasticsearch; \
    groupadd -f ${ES_GROUP} && useradd ${ES_USER} -s /bin/bash -g ${ES_GROUP}; \
    shasum -a 512 -c elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz.sha512; \
    tar xfz elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz; \
    cd elasticsearch-${ES_VERSION}/;
EXPOSE 9100 9200
RUN chown -R ${ES_USER}:${ES_GROUP} /usr/share/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /var/log/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /var/lib/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /etc/default/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /etc/elasticsearch/
CMD ["/bin/bash"]
```

Текст корня
```
{
  "name" : "netology_test",
  "cluster_name" : "netology_pandamys",
  "cluster_uuid" : "9Ubzx_zdQRC9h8wuOanppw",
  "version" : {
    "number" : "8.0.1",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "801d9ccc7c2ee0f2cb121bbe22ab5af77a902372",
    "build_date" : "2022-02-24T13:55:40.601285296Z",
    "build_snapshot" : false,
    "lucene_version" : "9.0.0",
    "minimum_wire_compatibility_version" : "7.17.0",
    "minimum_index_compatibility_version" : "7.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

# Задание 2

# Задание 3