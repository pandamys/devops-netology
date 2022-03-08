# Задание 1
Содержимое файла Dockerfile
```
FROM centos:7
ENV container docker
COPY elasticsearch.yml /usr/share/elasticsearch/config
WORKDIR /usr/share/elasticsearch
RUN yum -y install wget tar perl-Digest-SHA shasum
RUN wget https://download.java.net/java/GA/jdk17/0d483333a00540d886896bac774ff48b/35/GPL/openjdk-17_linux-x64_bin.tar.gz; \
    tar xvf openjdk-17_linux-x64_bin.tar.gz; \
    mv jdk-17 /opt/
RUN groupadd -g 1000 elasticsearch && useradd elasticsearch -u 1000 -g 1000
ENV ES_JAVA_HOME /opt/jdk-17
RUN export ES_JAVA_HOME
ENV ES_USER elasticsearch
RUN export ES_USER
ENV ES_GROUP elasticsearch
RUN export ES_GROUP
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.1-darwin-x86_64.tar.gz; \
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.1-darwin-x86_64.tar.gz.sha512; \
    shasum -a 512 -c elasticsearch-8.0.1-darwin-x86_64.tar.gz.sha512; tar xfz elasticsearch-8.0.1-darwin-x86_64.tar.gz; \
    cd elasticsearch-8.0.1/;
EXPOSE 9200 9100
RUN mkdir /var/log/elasticsearch /var/lib/elasticsearch /etc/default/elasticsearch /etc/elasticsearch;
RUN chown -R elasticsearch:elasticsearch /usr/share/elasticsearch/; \
    chown -R elasticsearch:elasticsearch /var/log/elasticsearch/; \
    chown -R elasticsearch:elasticsearch /var/lib/elasticsearch/; \
    chown -R elasticsearch:elasticsearch /etc/default/elasticsearch/; \
    chown -R elasticsearch:elasticsearch /etc/elasticsearch/
CMD ["/usr/share/elasticsearch/elasticsearch-8.0.1/bin/elasticsearch"]
```

# Задание 2

# Задание 3