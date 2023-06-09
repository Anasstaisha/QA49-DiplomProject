# Дипломный проект по профессии «Тестировщик»
***
#### Дипломный проект заключается в автоматизации тестирования комплексного сервиса, взаимодействующего с СУБД и API Банка.
Тестируемое приложение представляет собой веб-сервис, который предоставляет возможность купить тур по определённой цене с помощью двух способов:
* Обычная оплата по дебетовой карте
* Уникальная технология: выдача кредита по данным банковской карты

### Необходимое ПО для процедуры запуска автотестов:
* Docker
* IntelliJ IDEA
* JDK 11

### Шаги для запуска автотестов
1. Откройте терминал и запустите контейнер, в котором разворачиваются базы данных (MySQL и PostgreSQL) командой "docker-compose up";
2. Убедитесь, что необходимые базы данных были запущены командой "docker ps -a";
3. Откроте новую сессию в терминале и, в зависимости от запускаемой базы данных, запустите SUT:
    * командой java "-Dspring.datasource.url=jdbc:mysql://localhost:3306/data" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass" -jar ./artifacts/aqa-shop.jar **для MySQL**;
    * командой java "-Dspring.datasource.url=jdbc:postgresql://localhost:5432/data" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass" -jar ./artifacts/aqa-shop.jar **для PostgreSQL**.
4. Запустите тесты, открыв новую сессию терминала командой:
    * .\gradlew clean test "-Dsource=jdbc:mysql://localhost:3306/data" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass", если раннее запускали SUT **для MySQL**;
    * .\gradlew clean test "-Dsource=jdbc:postgresql://localhost:5432/data" "-Dspring.datasource.username=app" "-Dspring.datasource.password=pass", если раннее запускали SUT **для PostgreSQL**.
5. Запустите команду .\gradlew allureserve **для просмотра Allure отчетов**;
6. Нажмите комбинацию "Ctrl+C", ответив на последующий запрос "y" **для остановки Allure**;
7. Закройте терминал, в котором запускался SUT и выполните шаги 3-6 **для проверки второй базы данных**;
8. Запустите команду "docker-compose down" в терминале **для остановки контейнеров**.
