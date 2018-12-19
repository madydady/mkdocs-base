В данном документе описывается значение поля `content` для API описанном в Описание TransportServer HTTP Rest API v1.1.
Т.е. здесь описаны все возможные значения поля content в API транспортного уровня.


# Поле сontent (тело сообщения)

## Общий вид объекта

```
{
    type,
    clientId,
    threadId,
    appMarker,
    ...optional   
}
```

##### Описание параметров

| Параметр      | Тип    | Описание                                  |  
|---------------|--------|-------------------------------------------|
| `type`        | string | Тип сообщения                             |
| `clientId`    | string | Идентификатор клиента авторизованной зоны |
| `threadId`    | string | Идентификатор треда                       |
| `appMarker`   | string | Идентификатор приложения                  |
| `...optional` | -      | Прочие параметры сообщения                |


## Запросы

### Инициализация чата

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'INIT_CHAT',
        clientId,
        threadId,
        appMarker,
    },
    systemType: true
}
```

### Информация о клиенте

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'CLIENT_INFO',
        clientId,
        threadId,
        appMarker,
        appName,
        browser,
        cookie,
        device,
        engine,
        java,
        libVersion,
        os,
        referrer,
        screenDepth,
        screenHeight,
        screenWidth,
        url,
        geolocation,
        ip,
        phone,
        email,
        name,
        text
    },
    systemType: true
}
```

##### Описание параметров

| Параметр       | Тип    | Описание                                                                                           |  
|----------------|--------|----------------------------------------------------------------------------------------------------|
| `geolocation`  | string | Координаты клиента вида `"50.8578614,80.10485820000001"`                                           |  
| `ip`           | string | IP клиента                                                                                         |
| `appName`      | string | Название клиентского приложения                                                                    | 
| `browser`      | string | Название браузера и его версия                                                                     | 
| `clientLocale` | string | Двухбуквенный код локали клиента                                                                   | 
| `cookie`       | bool   | Поддержка браузером cookies                                                                        | 
| `device`       | string | Тип устройства клиента                                                                             | 
| `engine`       | string | Движок браузера                                                                                    | 
| `java`         | string | Поддержка браузером Java                                                                           | 
| `libVersion`   | string | Версия клиентского приложения                                                                      | 
| `os`           | string | Операционная система                                                                               | 
| `referrer`     | string | HTTP referer                                                                                       | 
| `screenDepth`  | string | Разрядность дисплея                                                                                | 
| `screenHeight` | string | Высота дисплея                                                                                     | 
| `screenWidth`  | string | Ширина дисплея                                                                                     | 
| `url`          | string | Текущий URL                                                                                        | 
| `email`        | string | E-mail клиента                                                                                     | 
| `name`         | string | Имя клиента                                                                                        | 
| `text`         | string | Текст сообщения, которое может быть отправлено клиентом, если чат находится в режиме недоступности | 


### Клиент набирает текст

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'TYPING',
        clientId,
        threadId,
        appMarker,
    },
    systemType: true
}
```


### Отправка сообщения

```
{
    deviceAddress: { deviceAddress }
    content: {
        clientId,
        threadId,
        appMarker,
        client: { 
            name 
        },
        text,
        quotes,
        attachments
    }
}
```
example:
{"client":{},"text":"текст сообщения","quotes":[],"attachments":[],"threadId":null}


##### Описание параметров

| Параметр      | Тип    | Описание                                    |  
|---------------|--------|---------------------------------------------|
| `client.name` | string | Имя клиента                                 |  
| `text`        | string | Текст сообщения                             |  
| `quotes`      | array  | Цитируемые сообщения                        |  
| `attachments` | array  | Вложения                                    |  
| `appMarker`   | string | Иденификатор приложения, может отсутсвовать |


#### Цитируемые сообщения (поле `quotes`)

Элемент массива цитируемых сообщений имеет следующий формат:

```
{
    providerId,
    text,
    sentAt,
    client: {
        name
    },
    attachments,
    receivedDate
}    
```

##### Описание параметров

| Параметр        | Тип    | Описание                             |  
|-----------------|--------|--------------------------------------|
| `providerId`    | string | Идентификатор сообщения на платформе | 
| `text`          | string | Текст сообщения                      | 
| `sentAt`        | string | Время отправки                       | 
| `client.name`   | string | Имя клиента                          | 
| `attachments`   | array  | Вложения цитаты                      | 
| `receivedDate`  | array  | Время доставки                       | 


#### Вложения (поле `attachments`)

Элемент массива вложений имеет следующий формат:

```
{
    result,
    optional: {
        name,
        type,
        size
    },
    name,
    type,
    size
}    
```

##### Описание параметров

| Параметр        | Тип    | Описание                           |  
|-----------------|--------|------------------------------------|
| `result`        | string | Идентификатор вложения в Datastore | 
| `optional.name` | string | Оригинальное название файла        | 
| `optional.type` | string | MIME-тип файла                     | 
| `optional.size` | string | Размер файла в байтах              | 


### Бинарный опрос

Клиент имеет возможность завершить диалог или продолжить общение.


#### Завершить тред

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'CLOSE_THREAD',
        clientId,
        threadId,
        appMarker,
    },
    systemType: true
}
```

#### Продолжить диалог

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'REOPEN_THREAD',
        clientId,
        threadId,
        appMarker,
    },
    systemType: true
}
```

### Реакция на получение опроса клиентом

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'SURVEY_PASSED',
        clientId,
        threadId,
        appMarker,
        sendingId
    },
    systemType: true
}
```

##### Описание параметров

| Параметр    | Тип    | Описание                      |  
|-------------|--------|-------------------------------|
| `sendingId` | number | Идентификатор текущего опроса |  


### Отправка результа опроса

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'SURVEY_QUESTION_ANSWER',
        clientId,
        threadId,
        appMarker,
        sendingId,
        questionId,
        text,
        rate,
        simple,
        scale,
        quotes
    },
    systemType: true
}
```

##### Описание параметров

| Параметр      | Тип    | Описание                                     |  
|---------------|--------|----------------------------------------------|
| `attachments` | array  | Вложения сообщения. См. *Отправка сообщения* |  
| `quotes`      | array  | Цитаты сообщения. См. *Отправка сообщения*   |  
| `scale`       | nnmber | Размер шкалы опроса, баллы                   |  
| `simple`      | bool   | Тип опроса                                   |  
| `rate`        | number | Оценка, баллы                                |  
| `text`        | string | Текст сообщения. См. *Отправка сообщения*    |  
| `sendingId`   | number | Идентификатор текущего опроса                |  
| `questionId`  | number | Идентификатор типа опроса                    |  


### Отключение клиента

```
{
    deviceAddress: { deviceAddress }
    content: {
        type: 'CLIENT_OFFLINE',
        clientId,
        threadId,
        appMarker,
    },
    systemType: true
}
```
