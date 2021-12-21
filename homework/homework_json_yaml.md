# Домашнее задание к занятию "4.3. Языки разметки JSON и YAML"


## Обязательная задача 1
Мы выгрузили JSON, который получили через API запрос к нашему сервису:
```
    { "info" : "Sample JSON output from our service\\t",
        "elements" :[
            { "name" : "first",
            "type" : "server",
            "ip" : 7175 
            },
            { "name" : "second",
            "type" : "proxy",
            "ip" : "71.78.22.43"
            }
        ]
    }
```
Экранировал спец.символы, добавил парочку кавычек и запятую

Нужно найти и исправить все ошибки, которые допускает наш сервис

## Обязательная задача 2
В прошлый рабочий день мы создавали скрипт, позволяющий опрашивать веб-сервисы и получать их IP. К уже реализованному функционалу нам нужно добавить возможность записи JSON и YAML файлов, описывающих наши сервисы. Формат записи JSON по одному сервису: `{ "имя сервиса" : "его IP"}`. Формат записи YAML по одному сервису: `- имя сервиса: его IP`. Если в момент исполнения скрипта меняется IP у сервиса - он должен так же поменяться в yml и json файле.

Скрипт в части JSON уже был написан, поэтому дополнил только выгрузку в YAML
### Ваш скрипт:
```python
import socket
import json
import yaml


def check_availability_service(temp_services, old_ip):
    dict_services = {}

    for service in temp_services:
        try:
            ip_service = socket.gethostbyname(service)
        except socket.gaierror:
            ip_service = "not resolved"
        dict_services[service] = ip_service
        if ip_service != old_ip[service]:
            print(f"""[ERROR] {service} IP mismatch: {old_ip[service]} {ip_service}""")
        else:
            print(f"""{service} - {ip_service}""")
    open("services.json", "w")
    return dict_services


def read_old_values():
    temp = json.load(open("services.json", "r"))
    return temp


def write_new_values(temp_dict):
    file = open("services.json", "w")
    file_yaml = open("services.yaml", "w")
    json.dump(temp_dict, file)
    yaml.dump(temp_dict, file_yaml)


services = ('drive.google.com', 'mail.google.com', 'google.com')
old_ip_services = read_old_values()
current_ip_services = check_availability_service(services, old_ip_services)
write_new_values(current_ip_services)
```

### Вывод скрипта при запуске при тестировании:
```
drive.google.com - 64.233.161.194
mail.google.com - 64.233.165.83
google.com - 64.233.162.100
```

### json-файл(ы), который(е) записал ваш скрипт:
```json
{"drive.google.com": "64.233.161.194", "mail.google.com": "64.233.165.83", "google.com": "64.233.162.100"}
```

### yml-файл(ы), который(е) записал ваш скрипт:
```yaml
drive.google.com: 64.233.161.194
google.com: 64.233.162.100
mail.google.com: 64.233.165.83
```