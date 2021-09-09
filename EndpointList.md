
В списках ошибок представлены не все возможные с точки зрения сервера ошибки, а те которые специфичны для эндпоинта. При этом необходимо обрабатывать и общие для всего сервера ошибки ( 500 / неверная сессия (если требуется авторизация) и тд )
в POST и PUT запросах параметры пердеаются в теле запроса, закодированными в JSON

base URL:     `https://restfulapi.ru/api/v2/`

---

# login - service [POST]
`/auth/{serviceId}/` -> [AuthObject](./Objects/Common.md)

#### POST params:
| param | type | description |
| ----- | ---- | ----------- | 
| serviceLogin | string | university service login |
| servicePassword | string | university service password |

**possible errors:**

| code  | condition |
| ----- | --------- |
| validation_error | сервис не смог авторизоваться с этими логином и паролем |
| not_found (404) | такого сервиса не существует |

---
# login - vk [POST]
`/auth/vk/` -> [AuthObject](./Objects/Common.md)


#### POST params:
| param | type | description |
| ----- | ---- | ----------- | 
| token | string | vk token |

**possible errors:**

| code  | condition |
| ----- | --------- |
| validation_error | токен вк протух или не валидный |

---

# University list [GET]
`/universities/`  -> [List\<University>](./Objects/University.md)

#### GET params:
*[default list params](./CRUDL.md)*



**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---

# single university [GET]
`/universities/{universityId}` -> [University](./Objects/University.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |

---

# professor list [GET]
`/universities/{universityId}/professors/` -> [List\<SchedUser>](./Objects/SchedUser.md)

#### GET params:
*[default list params](./CRUDL.md)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---

# group list [GET]
`/universities/{universityId}/groups/` -> [List\<SchedUser>](./Objects/SchedUser.md)

#### GET params:
*[default list params](./CRUDL.md)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---
# single schedUser [GET]
`/universities/{universityId}/schedUsers/{schedUserId}` -> [SchedUser](./Objects/SchedUser.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такого шедюзера не существует |

---
# Schedule [GET]
`/universities/{universityId}/schedule/{scheduleUserId}`  -> [List\<Lesson>](./Objects/Lesson.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такого шедюзера не существует |

# Lesson [GET]
`/universities/{universityId}/lessons/{lessonId}`  -> [Lesson](./Objects/Lesson.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такой пары не существует |

---

# Feed (сводка) [GET] Requires X-Session-Id header
 
`/feed`  -> [List\<FeedItem>](./Objects/FeedItem.md)

---

# Feed (новостная лента) [GET]  Requires X-Session-Id header
`/feed/{feedSourceId}/` -> [List\<FeedItem>](./Objects/FeedItem.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого фидсорса не существует |
| forbidden | не передана или передана некорректная сессия |

---

# Feed sources [GET]  Requires X-Session-Id header
`/feed/sources/` -> [List\<FeedSource>](./Objects/FeedSource.md)

#### GET params:
*[default list params](./CRUDL.md)*


**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |
| forbidden | не передана или передана некорректная сессия |

---

# single FeedSource [GET; PUT] Requires X-Session-Id header
`/feed/sources/{feedSourceId}` -> [FeedSource](./Objects/FeedSource.md)

#### PUT params:
| param | type | description |
| ----- | ---- | ----------- | 
| isEnabled | Bool | sets feed source enabled for current user |

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого фидсорса не существует |
| validation_error | не передан параметр isEnabled |
| forbidden | не передана или передана некорректная сессия |

---

# Deadlines [GET] Requires X-Session-Id header
`/deadlines/` -> [List\<Deadline>](./Objects/Deadline.md)

#### GET params:
*[default list params](./CRUDL.md)* 

| param | type |  description |
| ----- | ---- | ----------- | 
| externalSource | string | if set, get tasks from external source |

**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |
| not_found (404) | переданного дедлайн сорса не существует |
| forbidden | не передана или передана некорректная сессия |

---

# single Deadline  [POST] Requires X-Session-Id header
`/deadlines/` -> [Deadline](./Objects/Deadline.md)

#### POST params:

| param | type |  description |
| ----- | ---- | ----------- | 
| title | string | deadline title |
| description | varchar(250) | deadline description text; nullable |
| date | int64 | unix time of deadline date |
| subjectId | string | id of associated subject; nullable |

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует (только для обновления)|
| validation_error | передан пустой тайтл |
| validation_error | переданная дата < текущей |
| validation_error | некорректный subjectId |
| forbidden | не передана или передана некорректная сессия |


# single Deadline  [GET; DELETE; PUT] Requires X-Session-Id header
`/deadlines/{deadlineId}/` -> [Deadline](./Objects/Deadline.md)

#### PUT/ POST params:

| param | type |  description |
| ----- | ---- | ----------- | 
| title | string | deadline title |
| description | varchar(250) | deadline description text; nullable |
| date | int64 | unix time of deadline date |
| subjectId | string | id of associated subject; nullable |

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует (только для обновления)|
| validation_error | передан пустой тайтл |
| validation_error | переданная дата < текущей |
| validation_error | некорректный subjectId |
| forbidden | не передана или передана некорректная сессия |

---

# close deadline: [POST] Requires X-Session-Id header
`/deadlines/{deadlineId}/close`-> [Deadline](./Objects/Deadline.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует |
| forbidden | не передана или передана некорректная сессия (например удаляем дедлайн чужого юзера) |

# restart deadline: [DELETE] Requires X-Session-Id header
`/deadlines/{deadlineId}/close`-> [Deadline](./Objects/Deadline.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует |
| forbidden | не передана или передана некорректная сессия |

---

# Deadline sources [GET] Requires X-Session-Id header
`/deadlines/sources` -> [List\<DeadlineSource>](./Objects/DeadlineSource.md)
*[default list params](./CRUDL.md)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |
| forbidden | не передана или передана некорректная сессия |

---

# single Deadline source [GET] Requires X-Session-Id header
`/deadlines/sources/{SourceId}` -> [DeadlineSource](./Objects/DeadlineSource.md)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa сорса не существует |
| forbidden | не передана или передана некорректная сессия |

---
---
# USER [GET; PUT] Requires X-Session-Id header
`/me` -> [User](./Objects/User.md)

#### PUT params:

| param | type | description |
| ----- | ---- | ----------- | 
| universityId | string | set university by id and if schedUser is not sent, set schedUser to null |
| schedUserId | string | set schedUser from current university |


| param | type | description |
| ----- | ---- | ----------- | 
| serviceLogin | string | auth in university service |
| servicePassword | string | password for auth |

**possible errors:**

| code  | condition |
| ----- | --------- |
| validation_error | сервис не смог авторизоваться с этими логином и паролем |
| validation_error | неверный id универа |
| validation_error | неверный id шедюзера |
| syntax_error | некорректный синтаксис для data |
| forbidden | не передана или передана некорректная сессия |
