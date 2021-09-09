
В списках ошибок представлены не все возможные с точки зрения сервера ошибки, а те которые специфичны для эндпоинта. При этом необходимо обрабатывать и общие для всего сервера ошибки ( 500 / неверная сессия (если требуется авторизация) и тд )
в POST и PUT запросах параметры пердеаются в теле запроса, закодированными в JSON

base URL:     `https://restfulapi.ru/api/v2/`

---

# login - service [POST]
`/auth/{serviceId}/` -> [AuthObject](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Common-Objects-4Tznuj2OwpuT)

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
`/auth/vk/` -> [AuthObject](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Common-Objects-4Tznuj2OwpuT)


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
`/universities/`  -> [List<University>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/University)

#### GET params:
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)*



**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---

# single university [GET]
`/universities/{universityId}` -> [University](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/University)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |

---

# professor list [GET]
`/universities/{universityId}/professors/` -> [List<SchedUser>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/SchedUser)

#### GET params:
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---

# group list [GET]
`/universities/{universityId}/groups/` -> [List<SchedUser>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/SchedUser)

#### GET params:
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| syntax_error | ошибка в синтаксисе запроса на получение списка |

---
# single schedUser [GET]
`/universities/{universityId}/schedUsers/{schedUserId}` -> [SchedUser](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/SchedUser)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такого шедюзера не существует |

---
# Schedule [GET]
`/universities/{universityId}/schedule/{scheduleUserId}`  -> [List<Lesson>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Lesson)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такого шедюзера не существует |

# Lesson [GET]
`/universities/{universityId}/lessons/{lessonId}`  -> [Lesson](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Lesson)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого универа не существует |
| not_found (404) | такой пары не существует |

---

# Feed (сводка) [GET] Requires X-Session-Id header
 
`/feed`  -> [List<FeedItem>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/FeedItem)

---

# Feed (новостная лента) [GET]  Requires X-Session-Id header
`/feed/{feedSourceId}/` -> [List<FeedItem>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/FeedItem)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | такого фидсорса не существует |
| forbidden | не передана или передана некорректная сессия |

---

# Feed sources [GET]  Requires X-Session-Id header
`/feed/sources/` -> [List<FeedSource>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/FeedSource)

#### GET params:
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)*


**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |
| forbidden | не передана или передана некорректная сессия |

---

# single FeedSource [GET; PUT] Requires X-Session-Id header
`/feed/sources/{feedSourceId}` -> [FeedSource](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/FeedSource)

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
`/deadlines/` -> [List<Deadline>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Deadline)

#### GET params:
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)* 

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
`/deadlines/` -> [Deadline](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Deadline)

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
`/deadlines/{deadlineId}/` -> [Deadline](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Deadline)

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
`/deadlines/{deadlineId}/close`-> [Deadline](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Deadline)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует |
| forbidden | не передана или передана некорректная сессия (например удаляем дедлайн чужого юзера) |

# restart deadline: [DELETE] Requires X-Session-Id header
`/deadlines/{deadlineId}/close`-> [Deadline](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/Deadline)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa не существует |
| forbidden | не передана или передана некорректная сессия |

---

# Deadline sources [GET] Requires X-Session-Id header
`/deadlines/sources` -> [List<DeadlineSource>](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/DeadlineSource)
*[default list params](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/CRUDL)*

**possible errors:**

| code  | condition |
| ----- | --------- |
| syntax_error | ошибка в синтаксисе запроса на получение списка |
| forbidden | не передана или передана некорректная сессия |

---

# single Deadline source [GET] Requires X-Session-Id header
`/deadlines/sources/{SourceId}` -> [DeadlineSource](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/DeadlineSource)

**possible errors:**

| code  | condition |
| ----- | --------- |
| not_found (404) | переданного дедлайнa сорса не существует |
| forbidden | не передана или передана некорректная сессия |

---
---
# USER [GET; PUT] Requires X-Session-Id header
`/me` -> [User](https://scheduleapp.jetbrains.space/p/sa/documents/20/a/User)

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
