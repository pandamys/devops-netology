#Задание 1
1. Создал проект через кнопку "create new project"
2. Скачал пакет
```doctest
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-4.7.0.2747-linux.zip
unzip sonar-scanner-4.7.0.2747-linux.zip
mv ./sonar-scanner-4.7.0.2747-linux /opt
```
3. Добавляем путь
```doctest
export PATH="/opt/sonar-scanner-4.7.0.2747-linux/bin/:$PATH"
```
4. Получили версию
```doctest
vagrant@vagrant:~$ sonar-scanner --version
INFO: Scanner configuration file: /opt/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
INFO: Project root configuration file: NONE
INFO: SonarScanner 4.7.0.2747
INFO: Java 11.0.14.1 Eclipse Adoptium (64-bit)
INFO: Linux 5.4.0-100-generic amd64
```
5. Поправил конфиг
```doctest
nano /opt/sonar-scanner-4.7.0.2747-linux/conf/sonar-scanner.properties
```
Запускаем проверку
```doctest
sonar-scanner -Dsonar.coverage.exclusions=fail.py -Dsonar.login=97ab6ec36b9a8f0cd3e0b9b1905f073e5c2fb60e
```
6. Sonar показал, что есть две ошибки и один warning:
- неправильное инкрементирование и действия с переменной до её объявления;
- не используемая переменная pass
7. Меняем знак "=+" на "+=" и убираем pass;
8. Ошибки исправлены, тест прошёл успешно;

# Задание 2
1) Делаем следующие действия:
- Нажимаем кнопку "Upload";
- Выбираем maven-releases;
- Заполняем поля нужными данными и прикрепляем нужный нам файл;
2) Делаем то же самое для второй версии файла;
3) Проверяем через кнопку "Browse", раздел maven-public;

# Задание 3
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.netology.app</groupId>
    <artifactId>simple-app</artifactId>
    <version>1.0-SNAPSHOT</version>
    <repositories>
        <repository>
        <id>my-repo</id>
        <name>maven-public</name>
        <url>http://localhost:8081/repository/maven-public/</url>
        </repository>
    </repositories>
    <dependencies>
        <dependency>
        <groupId>netology</groupId>
        <artifactId>java</artifactId>
        <version>8_282</version>
        <classifier>distrib</classifier>
        <type>tar.gz</type>
        </dependency>
    </dependencies>
</project>
```