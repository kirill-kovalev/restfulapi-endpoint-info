# Deadline

| name  | type  | description |
| ------ | ------ | ------ |
| _id | string | unique object id |
| title | string | deadline name | 
| description | string | description of deadline |
| startDate | int64 | unixtime of date when deadline was created | 
| endDate | int64 | unixtime of date when deadline should be closed or push notification sent | 
| isExternal | bool | shows if deadline is external |
| isClosed | bool | set true or false only by user |
| subject | Subject | subject objecе associated with deadline |
| | | **следующие поля опциональны - могут и не прийти** |
| curPoints | int | current mark for  external Task |
| type | String | type of task from university service |
| markpoint | int | maximum mark for  external Task |
| reportRequired | bool | shows if it's possible to send reports to Task |
| files | [File] | array of files associated with Task |
