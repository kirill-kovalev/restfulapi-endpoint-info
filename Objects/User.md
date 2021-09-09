# User 

| name  | type  | description |
| ------ | ------ | ------ |
| _id | string | unique object id |
| firstName | string | |
| lastName | string | |
| avatar | string | user avatar URL |
| serviceLogin | string | login in university service | 
| vkId | int32 | users vk id 0 if null |
| isAdsEnabled | bool | flag to show or hide ads in app |
| **hasCards** | bool | flag that shows if cards screen should be displayed to user |
| university | University | user's University object |
| scheduleUser | SchedUser | users's grou or professor object | 
