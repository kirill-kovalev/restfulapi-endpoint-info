# Response<T>

Базовый корневой объект ответа. Любой ответ от сервера должен соответствовать этому формату. Параметр `T` - тот самый возвращаемый объект, который должен бытьвыведен в поле result. 
ошибка должна соответствовать формату объекта Error

| name  | type  | description |
| ------ | ------ | ------ |
| result | T | response result object |
| error | Error | error object ( null in no errors ) |

```
{
   "result": {
       ...
   },
   "error": null
}
```

# Error

объект ошибки. Возвращается внутри ResultObject в случае ошибки сервера. Если ошибки нет, поле Response.error примет значение null

| name  | type  | description |
| ------ | ------ | ------ |
| code | string | server error name, listed in errors file |
| id | double | error unique id in format xxx.xxx |
| message | string | localized message shown to user |
| data | JSON | json object with error specific data |


# AuthObject

объект возвращаемый во время авторизации. 

| name  | type  | description |
| ------ | ------ | ------ |
| sessionId | string | new session token |
| user | User | user object |


# ListObject<T>

объект возвращаемый при получении списков

| name | type | description |
| ---- | ---- | ---- |
| items | [T] | array of T objects with query, sort and pagination |
| totalCount | int | total count with query but without pagination |







































