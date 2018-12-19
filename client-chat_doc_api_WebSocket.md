# Общая структура ответа

```
{
    origin: "threads",
    type,
    ...payload
}
``` 

| Параметр     | Описание                                 |
|--------------|------------------------------------------|
| `origin`     | Идентификатор отправителя пуша           |
| `type`       | Тип собщения                             |
| `...payload` | Прочие поля, зависящие от типа сообщения |


# Типы сообщений

## `THREAD_OPENED`

Начало переписки

```
{
    origin: "threads",
    type: "THREAD_OPENED",
    threadId: <threadId>
}
``` 

### Payload

| Параметр   | Описание            |
|------------|---------------------|
| `threadId` | Идентификатор треда |


## `THREAD_CLOSED`

Тред завершен

            
## `TYPING`

Оператор набирает текст сообщения            


## `SURVEY`

Получен опрос

```
{
    origin: "threads",
    type: "SURVEY",
    text: "<survey_params>"
}
``` 

### Payload

| Параметр | Описание                                   |
|----------|--------------------------------------------|
| `text`   | Параметры опроса. JSON-строка              |


## `SCHEDULE`

Изменения в режиме доступности чата

```
{
    origin: "threads",
    type: "SCHEDULE",
    text: "<schedule_params>"
}
``` 

### Payload

| Параметр | Описание                                                |
|----------|---------------------------------------------------------|
| `text`   | Расписание работы чата для текущего канала. JSON-строка |
                                                                
                                     
## `MESSAGE`

Входящее собщение

```
{
    origin: "threads",
    type: "MESSAGE",
    attachments: [<attachments>],
    backendId: <backendId>,
    providerId: "<providerId>",
    display: <display>,
    operator: {
        gender: "<gender>",
        id: <id>,
        name: "<name>",
        photoUrl: "<photoUrl>",
        status: <status>,
    },
    quickReplies: [<quickReplies>],
    receivedDate: "<receivedDate>",
    threadId: <threadId>,
    uuid: "<uuid>"    
}
``` 

### Payload

| Параметр            | Описание                                  |
|---------------------|-------------------------------------------|
| `text`              | Текст сообщения                           |
| `backendId`         | Внутренний идентификатор сообщения        |
| `providerId`        | Идентификатор сообщения платформы         |
| `display`           | Флаг, позволяющий скрыть сообщение        |
| `operator.gender`   | Пол оператора                             |
| `operator.id`       | Идентификатор оператора                   |
| `operator.name`     | Имя оператора                             |
| `operator.photoUrl` | Аватар оператора                          |
| `operator.status`   | Статус оператора                          |                                     
| `attachments`       | Массив, содержащий список вложений        |   
| `quickReplies`      | Массив, содержащий список быстрых ответов |   
| `receivedDate`      | Время отправки                            |   
| `threadId`          | Идентификатор треда                       |   
| `uuid`              | UUID сообщения                            |   


## `OPERATOR_JOINED`

Оператор присоединился к диалогу

```
{
    origin: "threads",
    type: "OPERATOR_JOINED",
    text: "<text>",
    backendId: <backendId>,
    providerId: "<providerId>",
    display: <display>,
    operator: {
        id: <id>,
        gender: "<gender>",
        name: "<name>",
        photoUrl: "<photoUrl>",
        status: "<status>
    }
}
``` 

### Payload

| Параметр            | Описание                           |
|---------------------|------------------------------------|
| `text`              | Сопроводительный текст             |
| `backendId`         | Внутренний идентификатор сообщения |
| `providerId`        | Идентификатор сообщения платформы  |
| `display`           | Флаг, позволяющий скрыть сообщение |
| `operator.gender`   | Пол оператора                      |
| `operator.id`       | Идентификатор оператора            |
| `operator.name`     | Имя оператора                      |
| `operator.photoUrl` | Аватар оператора                   |
| `operator.status`   | Статус оператора                   |
                                                     

## `OPERATOR_LEFT`

Оператор отключился

```
{
    origin: "threads",
    type: "OPERATOR_LEFT",
    text: "<text>",
    backendId: <backendId>,
    providerId: "<providerId>",
    display: <display>,
    operator: {
        id: <id>,
        gender: "<gender>",
        name: "<name>",
        photoUrl: "<photoUrl>",
        status: "<status>
    }
}
``` 

### Payload

| Параметр            | Описание                           |
|---------------------|------------------------------------|
| `text`              | Сопроводительный текст             |
| `backendId`         | Внутренний идентификатор сообщения |
| `providerId`        | Идентификатор сообщения платформы  |
| `display`           | Флаг, позволяющий скрыть сообщение |
| `operator.gender`   | Пол оператора                      |
| `operator.id`       | Идентификатор оператора            |
| `operator.name`     | Имя оператора                      |
| `operator.photoUrl` | Аватар оператора                   |
| `operator.status`   | Статус оператора                   |
                

## `SCENARIO`

Получен массив сценариев обслуживания

 ```
 {
     origin: "threads",
     type: "SCENARIO",
     text: "<scenario_params>"
 }
 ``` 

### Payload

| Параметр | Описание                                   |
|----------|--------------------------------------------|
| `text`   | Массив сценариев обслуживания. JSON-строка |
 
 
## `OPERATOR_LOOKUP_STARTED`

Начат поиск оператора    


## `REQUEST_CLOSE_THREAD`

 Запрос на завершение треда по таймауту
 
 ```
 {
     origin: "threads",
     type: "REQUEST_CLOSE_THREAD",
     hideAfter: "<hideAfter>"
 }
 ``` 

| Параметр    | Описание                                 |
|-------------|------------------------------------------|
| `hideAfter` | Время, после которого запрос будет скрыт |                   
                     

## `MESSAGES_READ`

Уведомление о том, что сообщения клиента были прочитаны оператором

### Payload

| Параметр             | Описание                                                                 |
|----------------------|--------------------------------------------------------------------------|
| `readInMessageIds`   | Строка, содержащая список идентификаторов сообщений, разделенных запятой |



       
