# Дипломный проект по профессии «Тестировщик»

Дипломный проект представляет собой автоматизацию тестирования комплексного сервиса, взаимодействующего с СУБД и API Банка.

## Документы
* [Задание](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/Task.md)
* [План автоматизации](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/Plan.md)
* [Отчет по итогам тестирования](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/Report.md)
* [Отчет по итогам автоматизированного тестирования](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer/blob/main/documentation/Summary.md)

## Приложения которые должны быть установлены на компьютере для корректного запуска проекта

* IntelliJ IDEA в комплекте с JDK 11
* Docker Desktop
* Dbeaver

## Процедура запуска авто-тестов:

**1.** Клонировать на локальный репозиторий [дипломный проект](https://github.com/Andrey-Shelikhanov/Diploma.QA.Engineer)

**2.** Запустить Docker Desktop

**3.** Открыть проект в IntelliJ IDEA

**4.** В терминале запустить контейнеры:

    docker-compose up -d

**5.** Запустить целевое приложение:

     для mySQL: 
    java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/app" -jar artifacts/aqa-shop.jar

     для postgresgl:
     java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/app" -jar artifacts/aqa-shop.jar

**6.** Проверить доступность приложения в браузере по адресу: http://localhost:8080/

**7.** Открыть второй терминал

**8.** Во втором терминале запустить тесты:

    для mySQL:
    ./gradlew clean test "-Ddb.url=jdbc:mysql://localhost:3306/app"

    для postgresgl: 
    ./gradlew clean test "-Ddb.url=jdbc:postgresql://localhost:5432/app"

**9.** Создать отчёт Allure и открыть в браузере:

    ./gradlew allureServe

**10.** Для завершения работы allureServe выполнить команду:

    Ctrl+C

и подтвердить действие в терминале вводом Y.

**11.** Для остановки работы контейнеров выполнить команду:

    docker-compose down

