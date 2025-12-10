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
<img width="1229" height="781" alt="Screenshot 2025-12-10 010345" src="https://github.com/user-attachments/assets/ef53f8b6-59f6-45e3-9bbb-df5b345cf0a3" />


### Деплой
Любой коммит в main запустит github actions, который соберёт контейнер и отправит его на yandex cloud.
Выглядит это так:
<img width="1832" height="875" alt="image" src="https://github.com/user-attachments/assets/b51177ac-d9af-4d05-b52f-8b8f3373ea5f" />

Контейнер успешно обновляется:
<img width="1411" height="714" alt="image" src="https://github.com/user-attachments/assets/cd32b7d5-c36b-43b9-8599-5161fc642b69" />

К сожалению, запрос на сервер обрабатывается http1.x, а grpc работает в 2.
<img width="1681" height="145" alt="image" src="https://github.com/user-attachments/assets/252e22b4-01b7-4a22-be4b-de0bbb3e70de" />
