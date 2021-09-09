# Lesson

| name  | type  | description |
| ------ | ------ | ------ |
| _id | string | unique object id |
| day | enum(sun,mon,tue,wed,thu,fri,sat) | weekday of lesson | 
| week | enum(odd,even) | week type of lesson |
| startTime | string | string in format HH:mm of lesson start time|
| endTime | string | string in format HH:mm of lesson end time |
| lessonNum | Int32 | number of lesson |
| type | enum(lecture,lab,practice,test,course) | type of lesson |
| rooms | string | string with al rooms for this lesson |
| tags | [LessonTag] | array of tags for lesson |
| groups | [SchedUser] | array of groups that has this lesson |
| professors | [SchedUser] | array of professors that has this lesson |
| subject | Subject | subject associated with this lesson | 
