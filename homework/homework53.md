# Задание 1
- Я скачал нужный образ nginx
- Создал html-файл с нужным контекстом
- Создал Dockerfile с инструкциями скопировать мой index.html во внутрь docker-образа

```
  FROM nginx
  RUN apt-get update && apt-get install -y nano htop && \
  rm -rf /var/cache/apt/*
  WORKDIR /usr/share/nginx/html
  COPY ./index.html .
  CMD [ "nginx", "-v" ]
  STOPSIGNAL SIGQUIT
  CMD ["nginx", "-g", "daemon off;"]
```
- Создал Docker-образ на основе моего Dockerfile
```aidl
docker build -t pandamys/nginx_netology:1 .
```

- Запустил контейнер на основе моего образа (маппинг портов для тестирования)
```aidl
docker run -p 19999:80 --name nginx_netology pandamys/nginx_netology:1
```
- Получил требуемую страницу в качестве дефолтной. Отправил образ в докер-хаб
```aidl
https://hub.docker.com/repository/docker/pandamys/nginx_netology
```

# Задание 2
- Высоконагруженное монолитное java веб-приложение;\
Я думаю, что не очень подходит, так как java использует свою виртуальную машину и её ещё запускать в docker, схема выглядит сложной для высоконагруженного приложения, а также усложняется траблшутинг.
Лучше использовать полноценную ВМ.


- Nodejs веб-приложение;
Я думаю, что для простых веб-приложений docker подходит лучше всего, так как позволяет быстро отмасштабировать схему, предоставлять тестовую среду или перезапуститься в случае проблем.


- Мобильное приложение c версиями для Android и iOS;
Думаю, что для тестирования МП docker подходит хорошо, так как можно быстро собирать образы под разные версии мобильных ОС, полноценная виртуализация будет точно избыточной.


- Шина данных на базе Apache Kafka;
Никогда не работал с данным приложением, поэтому трудно оценить можно или нет. В интернете нашёл примеры инструкций для разворота, так что видимо вполне рабочий вариант для отказоустойчивости.


- Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;
Думаю, что вполне можно использовать, так как это опять же веб-приложение, а также готовый Docker image позволит быстрее развернуть стэк этих приложений, доработав образ лишь под какие-то свои нужды, не разбираясь со всеми взаимосвязями.


- Мониторинг-стек на базе Prometheus и Grafana;
Думаю, что также подходит, снова веб, не так чтобы сильно нагруженный. Опять же можно скачать готовый образ и развернуть намного быстрее, чем настраивать всё вручную.


- MongoDB, как основное хранилище данных для java-приложения;
Базу данных я бы не стал запускать из docker-образа, всё же отдал бы предпочтение ВМ, так как необходимо наибольшее быстродействие и отказоустойчивость.


- Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.
Снова веб-сервисы, где нет критичной нагрузки, поэтому думаю можно использовать Docker. И опять же есть официальный образ для быстрого разворачивания Gitlab.

# Задание 3
Всё получилось, на второй машине два файла в итоге получилось с тем содержанием, что я написал.
```bash
root@4337b9f203f5:/# ls -l /data/
total 8
-rw-r--r-- 1 root root 22 Feb  1 18:51 test_file
-rw-r--r-- 1 root root 22 Feb  1 18:51 test_file2
root@4337b9f203f5:/# cat /data/test_file2
Netology-Cool
root@4337b9f203f5:/#
```