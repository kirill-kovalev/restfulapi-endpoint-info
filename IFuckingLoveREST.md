## Краткая информация о взаимодействи с сервером 

Отправка запросов
---
1) Отправка запросов происходит по протоколу http(s)
2) Сервер принимает GET, POST, PUT, DELETE запросы. Какие конкретно запросы имеет смысл слать указано явно в списке эндрпоинтов ( но нет гарантий что неверный тип запроса хоть как-то обрабатывается )
3) для передачи параметров в GET запросах используется сам путь URL
4) для передачи параметров POST/PUT/DELETE и иже с ними используется JSON, передаваемый в теле запроса.

### Хедеры
* `X-Request-Id` - debug header; **Сервер должен вернуть то же самое значение. Используется для дебага**
* `X-Session-Id` - current user's token received from AuthObject; Must be sent in all requests that require auth


Авторизация 
---
Часть эндпоинтов доступна только после авторизации. Для авторизации необходимо отправитьзапрос авторизации на один из [доступных эндпонитов](), после чего в случае успеха вы получите ответ вроде такого
#### Request
```
curl --location --request POST 'http://restfulapi.ru/api/v2/auth/TEST' \
--header 'Content-Type: application/json' \
--data-raw '{
    "serviceLogin": "test",
    "servicePassword": "test"
}'
```
#### Response
```
{
    "result": {
        "sessionId": "4b879a7ebd7386qa2f497a52179453718092456862a66ccfc5926270d818d361",
        "user": {
            "_id": "2b86622a3da042c93fced9e42f400eb5f2db76aabf0969a01a0efca3fab7275e",
            "serviceLogin": "test",
            ...
            "vkId": null
        }
    },
    "error": null
}
```

Необходимо сохранить/запомнить sessionId.
При отправке последующих запросов данное значение надо передавать в хедере `X-Session-Id`
#### Request
```
curl --location --request GET 'https://restfulapi.ru/api/v2/deadlines?offset=0&limit=2' \
--header 'X-Session-Id: 2b86622a3da042c93fced9e42f400eb5f2db76aabf0969a01a0efca3fab7275e'
```

Получение ответов
---

необоходимая структура ответа описана в файле [Objects/Common.md](./Objects/Common.md)
Пересень возможных ошибок описан в файле [Errors.md](./Errors.md)

### Коды ответов

HTTP Code by [action](./CRUDL.md)

| action name | code | condition if exists | 
| ----------- | ---- |-------------------- |
| POST | 200 | successfully done |
| Create | 201 | successfully created |
| Update | 200 | successfully updated |
| Delete | 202 | successfully deleted |
| Read | 200 | object exists |
| List | 200 | list exists and not empty |

