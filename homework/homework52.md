# Задание 1
1.1. Используя паттерны IaaC позволяет на ранних этапах находить ошибки, так как код всегда актуален.\
Позволяет автоматически собирать проекты и накатывать их на тестовую систему. Уменьшая зависимость от людей необходимых для этого.\
1.2. Основополагающая - это CI, так как у наших разработчиков всегда актуальный код, у них будет меньше проблем при объединение всего в одну ветку и обнаружение, что после каких-то изменений их код стал неактуальным.

# Задание 2
1. Тем, что он не требует установки дополнительного ПО, а использует SSH для подключения на управляемый сервер.
2. Метод push более надёжный, потому что мы знаем, что наши результаты доставлены или выполнились с ошибкой. В методе pull сервер может недостучаться за изменениями и мы можем узнать об этом не сразу.

# Задание 3
1. 6.1.32
2. PS C:\temp\devops> vagrant --version
Vagrant 2.2.19
3. root@vagrant:/home/vagrant# ansible --version
ansible 2.9.6