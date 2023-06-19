# Реализация сервисов на php

Указанный набор технологий может меняться под конкретные нужды и задачи.

[Технологический радар](https://magnit-tech.github.io/magnit-online/tech/radar/php/index.html)

## Технологии

- Php >= 8.0
- Nginx + php-fpm - вебсервер
- Symfony LTS - как фреймворк
- Composer - пакетный менеджер для установки зависимостей
- Doctrine - в качестве основной ORM
- Guzzle - как библиотека для написания http клиентов до других API
- OpenAPI и GraphQL - как интерфейсы REST API
- Cron - планировщик
- Supervisor - для управления демонами
- Redis и Memcache - для кеша
- Mysql (Percona) и Postgres - если нужны реляционные БД
- Kafka, RabbitMQ, DB queue - для очередей
- PHPUnit - как фрейм для написания автоматических тестов
- Postman - что бы делиться подготовленными коллекциями по REST API
- Swagger - для автоматического сбора документации по REST API
- Twig - как шаблонизатор
- JIRA - как система для управления потоком задач
- Confluence - для документации

## Task flow in Git
- Задача = feature ветка
- Ветвимся от master
- Под релизы собираются ветки, которые после smoke сливаются с master
- Для именования веток используем № задачи из JIRA + Semantic Git Commit

## Как проверяем код и стандартизируем
- PSR - как список стандартов
- SonarQube - как статический анализатор
- PHP-CS-Fixer - для проверки стандартов

## Какое окружение для разработки

Проекты содержат docker-compose файл(-ы), с полностью описанными зависимыми сервисами и моккерами для запуска в Docker.
Make файл для удобства запуска одной командой.
Есть Dev, Test, Uat облачные среды под любые нужды.

## CI/CD

- pipeline для запуска SonarCube и PHP-CS-Fixer после commit-ов
- автоматическая сборка и упаковка докер образов: dev/test/uat/prod
- pipeline под запуск unit тестов
- функциональные тесты на Python
- ansible для Iac
- автоматическая доставка приложений на среды по тегам

## Внешние библиотеки

- Стараемся придерживаться Zero dependency подхода либо форкаем стабильные версии пакетов
- Автоматический обновление версий в composer вида {..^} запрещёны
- Ведём списки проверенных библиотек у которых проведён анализ кода

# Лучшие практики


* [DDD](https://en.wikipedia.org/wiki/Domain-driven_design)
* [Comment Code](https://stackoverflow.blog/2021/12/23/best-practices-for-writing-code-comments/)
* [Low cognitive complexity](https://docs.codeclimate.com/docs/cognitive-complexity)
* [CQRS](https://habr.com/ru/company/skyeng/blog/546314/) - простым языком
* [PHP-PSR](https://www.php-fig.org/psr/)
* [Symfony Right Way](https://symfony.com/doc/current/best_practices.html)
* [SOLID](https://ru.wikipedia.org/wiki/SOLID_(%D0%BE%D0%B1%D1%8A%D0%B5%D0%BA%D1%82%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D0%B5_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5))
* [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself)
* [KISS](https://ru.wikipedia.org/wiki/KISS_(%D0%BF%D1%80%D0%B8%D0%BD%D1%86%D0%B8%D0%BF))