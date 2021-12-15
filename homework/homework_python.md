# Домашнее задание к занятию "4.2. Использование Python для решения типовых DevOps задач"

## Обязательная задача 1

Есть скрипт:
```python
#!/usr/bin/env python3
a = 1
b = '2'
c = a + b
```

### Вопросы:
| Вопрос  | Ответ |
| ------------- | ------------- |
| Какое значение будет присвоено переменной `c`?  | Никакое, питон сругается, что мы пытаемся сложить число и строку  |
| Как получить для переменной `c` значение 12?  | Привести a к str: str(a) + b   |
| Как получить для переменной `c` значение 3?  | Привести b к int: a + int(b)  |

## Обязательная задача 2
Мы устроились на работу в компанию, где раньше уже был DevOps Engineer. Он написал скрипт, позволяющий узнать, какие файлы модифицированы в репозитории, относительно локальных изменений. Этим скриптом недовольно начальство, потому что в его выводе есть не все изменённые файлы, а также непонятен полный путь к директории, где они находятся. Как можно доработать скрипт ниже, чтобы он исполнял требования вашего руководителя?

```python
#!/usr/bin/env python3

import os

bash_command = ["cd ~/netology/sysadm-homeworks", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '')
        print(prepare_result)
        break
```

### Ваш скрипт:
```python
import os

bash_command = ["cd D:\Documents\devops-netology", "git status"]
result_os = os.popen(' && '.join(bash_command)).read()
is_change = False
for result in result_os.split('\n'):
    current_dir = os.getcwd()
    if result.find('modified') != -1:
        prepare_result = result.replace('\tmodified:   ', '').split("/")[1]
        print(current_dir + "/" + prepare_result)
        #break
```

### Вывод скрипта при запуске при тестировании:
```
D:\Documents\devops-netology\homework/homework_Bash.md
D:\Documents\devops-netology\homework/homework_python.md
```

## Обязательная задача 3
1. Доработать скрипт выше так, чтобы он мог проверять не только локальный репозиторий в текущей директории, а также умел воспринимать путь к репозиторию, который мы передаём как входной параметр. Мы точно знаем, что начальство коварное и будет проверять работу этого скрипта в директориях, которые не являются локальными репозиториями.

Преобразуем в функцию наш скрипт, которая принимает один обязательный параметр пути
### Ваш скрипт:
```python
import os

def check_modify_file(path):
    bash_command = ["cd " + path, "git status"]
    result_os = os.popen(' && '.join(bash_command)).read()
    is_change = False
    for result in result_os.split('\n'):
        current_dir = os.getcwd()
        if result.find('modified') != -1:
            prepare_result = result.replace('\tmodified:   ', '').split("/")[1]
            print(current_dir + "/" + prepare_result)
            #break
```

### Вывод скрипта при запуске при тестировании:
```
D:\Documents\devops-netology\homework/homework_Bash.md
D:\Documents\devops-netology\homework/homework_python.md
```

## Обязательная задача 4
1. Наша команда разрабатывает несколько веб-сервисов, доступных по http. Мы точно знаем, что на их стенде нет никакой балансировки, кластеризации, за DNS прячется конкретный IP сервера, где установлен сервис. Проблема в том, что отдел, занимающийся нашей инфраструктурой очень часто меняет нам сервера, поэтому IP меняются примерно раз в неделю, при этом сервисы сохраняют за собой DNS имена. Это бы совсем никого не беспокоило, если бы несколько раз сервера не уезжали в такой сегмент сети нашей компании, который недоступен для разработчиков. Мы хотим написать скрипт, который опрашивает веб-сервисы, получает их IP, выводит информацию в стандартный вывод в виде: <URL сервиса> - <его IP>. Также, должна быть реализована возможность проверки текущего IP сервиса c его IP из предыдущей проверки. Если проверка будет провалена - оповестить об этом в стандартный вывод сообщением: [ERROR] <URL сервиса> IP mismatch: <старый IP> <Новый IP>. Будем считать, что наша разработка реализовала сервисы: `drive.google.com`, `mail.google.com`, `google.com`.

Немного сложная реализация, но постарался сделать более универсально
### Ваш скрипт:
```python
import socket
import json


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
    json.dump(temp_dict, file)


services = ('drive.google.com', 'mail.google.com', 'google.com')
old_ip_services = read_old_values()
current_ip_services = check_availability_service(services, old_ip_services)
write_new_values(current_ip_services)

```

### Вывод скрипта при запуске при тестировании:
```
drive.google.com - 64.233.161.194
mail.google.com - 64.233.165.17
google.com - 64.233.162.138
```
```
drive.google.com - 64.233.161.194
[ERROR] mail.google.com IP mismatch: 0.0.0.0 64.233.165.83
[ERROR] google.com IP mismatch: 64.233.162.138 64.233.162.100
```