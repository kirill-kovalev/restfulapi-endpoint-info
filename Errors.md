# Errors

### Поле *code* в  объекте Error не может принимать иное значение кроме как одно из значений в таблице ниже
Значение из поля message должно выводиться конечному пользователю

| code | HTTP Code |  description |
| ---- | --------- | ----------- |
| invalid_api_version | 410 | unsupported api version used |
| not_found | 501 | endpoint doesn't exist |
| not_found | 404 | database object can not be found ( was deleted or not created )
| forbidden | 403 | X-Session-Id is outdated or invalid; on client user **MUST** be logouted |
| forbidden | 401 | X-Session-Id is required but not passed; on client try to logout
| too_often | 429 | throttling limit reached; request should be repeated after some time |
| validation_error | **XXX** | error while validating input data ( for example third-party services credentials are incorrect or input text is too long for field | 
| syntax_error | 500 | error in list request syntax ( or response scheme in future) |
| server_error | 500 | any other server error; HTTP code identofies the error type |
*To be continued*
