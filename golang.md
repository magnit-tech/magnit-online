# Golang service requirements

## Version

1.14 и выше. Версии обновлять только до stable.

## Logging

Используем https://github.com/uber-go/zap

Логирование только структурное.

Пример:

```go
l.Info("Test message", zap.String("details", "details_val"))
```

## Http framework

https://github.com/labstack/echo

## Postgresql

https://github.com/jackc/pgx

Не используем ORM, только RAW запросы.

Миграции:
https://github.com/golang-migrate/migrate

## Panic & recover

В обработчиках методов и в запускаемых goroutines должны быть recover. 

## Specification

Используем подход specification first(OpenAPI v3.0).

Http methods только **GET** | **POST**.

Именования методов:
```/$version/$domain/$action```

Например:
```/v1/users/add```

## Code generation

~~Для генерации используется инструмент~~

~~https://github.com/deepmap/oapi-codegen (ждем принятия PR чтобы починить генерацию)~~
```sh
git clone https://github.com/deepmap/oapi-codegen.git
git checkout 5f39b82d62
go install cmd/oapi-codegen/oapi-codegen.go
#generate types and server
oapi-codegen --generate types -o gen/types.go --package gen swagger.yaml
oapi-codegen --generate server -o gen/server.go  --package gen swagger.yaml
```
 