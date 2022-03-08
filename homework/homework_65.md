# Задание 1
Содержимое файла Dockerfile
```
FROM centos:7
ENV container docker
ENV ES_JAVA_HOME /opt/jdk-17
ENV ES_USER elasticsearch
ENV ES_GROUP elasticsearch
ENV ES_HOME /usr/share/elasticsearch
ENV ES_VERSION 8.0.1

WORKDIR ${ES_HOME}

COPY elasticsearch.yml /usr/share/elasticsearch-${ES_VERSION}/config/elasticsearch.yml

RUN wget https://download.java.net/java/GA/jdk17/0d483333a00540d886896bac774ff48b/35/GPL/openjdk-17_linux-x64_bin.tar.gz;
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.1-darwin-x86_64.tar.gz; \
    wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-8.0.1-darwin-x86_64.tar.gz.sha512; \

RUN tar xvf openjdk-17_linux-x64_bin.tar.gz; \
    mv jdk-17 /opt/;

RUN yum -y install wget tar perl-Digest-SHA shasum; \
    mkdir /var/log/elasticsearch /var/lib/elasticsearch /etc/default/elasticsearch /etc/elasticsearch; \
    groupadd -f ${ES_GROUP} && useradd ${ES_USER} -s /bin/bash -g ${ES_GROUP};

RUN shasum -a 512 -c elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz.sha512; \
    tar xfz elasticsearch-${ES_VERSION}-darwin-x86_64.tar.gz; \
    cd elasticsearch-${ES_VERSION}/;

EXPOSE 9200

RUN chown -R ${ES_USER}:${ES_GROUP} /usr/share/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /var/log/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /etc/default/elasticsearch/; \
    chown -R ${ES_USER}:${ES_GROUP} /etc/elasticsearch/

CMD ["${ES_HOME}/elasticsearch-${ES_VERSION}/bin/elasticsearch"]
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
ind-1
```
{
  "ind-1": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "1",
        "provided_name": "ind-1",
        "creation_date": "1646776279237",
        "number_of_replicas": "0",
        "uuid": "4BTN0inMQRukoJXgfxDNEA",
        "version": {
          "created": "8000199"
        }
      }
    }
  }
}
```

ind-2
```

  "ind-2": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "2",
        "provided_name": "ind-2",
        "creation_date": "1646776301940",
        "number_of_replicas": "1",
        "uuid": "yzzsBn_1SG-cBWmT776KpA",
        "version": {
          "created": "8000199"
        }
      }
    }
  }
}
```

ind-3
```
{
  "ind-3": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "4",
        "provided_name": "ind-3",
        "creation_date": "1646776327910",
        "number_of_replicas": "2",
        "uuid": "aqaZqIfURW2nYvfKHPpbnQ",
        "version": {
          "created": "8000199"
        }
      }
    }
  }
}
```

Жёлтый - означает, что не хватает реплик в онлайне.

# Задание 3
Запрос на создание репозитория
```
PUT https://127.0.0.1:9200/_snapshot/snapshots

{
  "type": "fs",
  "settings": {
    "location": "snapshots"
  }
}
```

Ответ
```
{
  "acknowledged": true
}
```

Все индексы
```
{
  "ind-1": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "1",
        "provided_name": "ind-1",
        "creation_date": "1646776279237",
        "number_of_replicas": "0",
        "uuid": "4BTN0inMQRukoJXgfxDNEA",
        "version": {
          "created": "8000199"
        }
      }
    }
  },
  "ind-2": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "2",
        "provided_name": "ind-2",
        "creation_date": "1646776301940",
        "number_of_replicas": "1",
        "uuid": "yzzsBn_1SG-cBWmT776KpA",
        "version": {
          "created": "8000199"
        }
      }
    }
  },
  "ind-3": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "4",
        "provided_name": "ind-3",
        "creation_date": "1646776327910",
        "number_of_replicas": "2",
        "uuid": "aqaZqIfURW2nYvfKHPpbnQ",
        "version": {
          "created": "8000199"
        }
      }
    }
  },
  "test": {
    "aliases": {},
    "mappings": {},
    "settings": {
      "index": {
        "routing": {
          "allocation": {
            "include": {
              "_tier_preference": "data_content"
            }
          }
        },
        "number_of_shards": "1",
        "provided_name": "test",
        "creation_date": "1646777619272",
        "number_of_replicas": "0",
        "uuid": "5Wb6tBgcTjKJ_GltvquIPg",
        "version": {
          "created": "8000199"
        }
      }
    }
  }
}
```

Запрос на создание снапшота
```
{
  "indices": "ind-1,ind-2,ind-3,test",
  "ignore_unavailable": true,
  "include_global_state": false,
  "metadata": {
    "taken_by": "user123",
    "taken_because": "backup before upgrading"
  }
}
```

Ответ
```
{
  "accepted": true
}
```

Файлы в папке с индексами
```
[root@6eeeacfb0e56 elasticsearch]# ll ./elasticsearch-8.0.1/snapshots/snapshots/
total 20
-rw-rw-r-- 1 elasticsearch elasticsearch 1425 Mar  8 22:17 index-0
-rw-rw-r-- 1 elasticsearch elasticsearch    8 Mar  8 22:17 index.latest
drwxrwxr-x 6 elasticsearch elasticsearch 4096 Mar  8 22:17 indices
-rw-rw-r-- 1 elasticsearch elasticsearch  202 Mar  8 22:17 meta-Xufbiu3GRZmARuEH1L31qw.dat
-rw-rw-r-- 1 elasticsearch elasticsearch  393 Mar  8 22:17 snap-Xufbiu3GRZmARuEH1L31qw.dat
```

Восстановление индекса
```
POST https://127.0.0.1:9200/_snapshot/snapshots/my_snapshot/_restore

{
  "indices": "test"
}
```

Ответ
```
{
  "accepted": true
}
```