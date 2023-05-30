# Golang

[Технологический радар](https://magnit-tech.github.io/magnit-online/tech/radar/golang/index.html)



## Version

1.17 и выше. Версии обновлять только до stable.

## GIT, Gitlab, CI/CD

* Репозитории проектов хранятся на gitlab.com.
* Все процессы CI/CD полностью автоматизированы. Вмешательство админов и devops'ов для деплоя сервисов не требуется.
* Новые микросервисы поднимаются из шаблонов и сразу готовы к деплою, даже без добавления бизнес-логики.
* Задачи, находящиеся в разработке, можно проверять и тестировать в виртуальных окружениях, которые автоматически создаются при пуше ветки в gitlab.

## Logging

Используем https://github.com/uber-go/zap

Логирование только структурное, логи пишем в JSON.
Для агрегации логов используем Loki. Просмотр логов осуществляется через Grafana и/или Kibana.

## Tracing

Используем актуальную версию клиента jaeger.
В качестве хранилища и бэкенда для трайсинга используется Grafana Tempo: https://grafana.com/oss/tempo/

## Metrics

Для метрик используем Prometheus.

## HTTP Framework

https://github.com/labstack/echo

## Postgresql

Работа с postgresql осуществляется с помощью: https://github.com/jackc/pgx

Не используем ORM, только RAW запросы.

Миграции накатываем с помощью golang-migrate: https://github.com/golang-migrate/migrate

## Specification

Для взаимодействия между сервисами используем подход specification first (OpenAPI v3.0).

Http methods только **GET** | **POST**.

Именования методов:
```/$version/$domain/$action```

Например:
```/v1/users/add```

## Code Generation

Для генерации клиентов использует oapi-codegen (https://github.com/deepmap/oapi-codegen) с набором своих доработок и исправлений.

## Testing

Для удобства написания тестов используем:
* testify toolkit: https://github.com/stretchr/testify
* mockery https://github.com/vektra/mockery
