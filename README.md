# Github actions + deploy to Yandex Cloud

### Локальный запуск контейнеров
Стартуем командой:
```
docker compose -f docker-compose.blue.yml -f docker-compose.green.yml
-f docker-compose.nginx.yml up
```
После этого можно запросить статус:
```
grpcurl -plaintext localhost:50055 PredictionService.Health
```
Ожидаемый результат 10% запросов уходит на green:


### Деплой
Любой коммит в main запустит github actions, который соберёт контейнер и отправит его на yandex cloud.
Выглядит это так:

Контейнер успешно обновляется:

К сожалению, запрос на сервер обрабатывается http1.x, а grpc работает в 2.