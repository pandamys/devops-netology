# Задание 1
## Задание 1.1.
1. Изменяемую архитектуру, так как ТЗ не чёткое и будет куча изменений, чтобы не пересобирать образы полностью.
2. На начальном этапе, пока клиент один, смысла в центральном сервере, скорей нет. Можно добавить в дальнейшем.
3. Думаю, что использовать решения без агентов.
4. Использовать совместное решение.

## Задание 1.2.
Я бы хотел использовать Terraform, Docker, Kubernetes, Ansible.

## Задание 1.3.
Я думаю, что выбранные инструменты покроют большинство вопросов. Но если кто-то из команды предложил бы рассмотреть какое-то решение ещё, то изучил бы и его в качестве альтернативы.

# Задание 2
Пришлось ставить через ВПН, но установил.
```doctest
root@vagrant:/home/vagrant# terraform --version
Terraform v1.1.7
on linux_amd64
```

# Задание 3
Скачиваем дистриб нужной версии и распаковываем.
```
root@vagrant:/home/vagrant# terraform --version
Terraform v1.1.7
on linux_amd64
root@vagrant:/home/vagrant# /opt/terraform_12/terraform --version
Terraform v0.12.31

Your version of Terraform is out of date! The latest version
is 1.1.7. You can update by downloading from https://www.terraform.io/downloads.html
root@vagrant:/home/vagrant#
```