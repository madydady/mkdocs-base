# Заголовки запросов к Datastore

## Формирование токена для заголовков

Токен формируется по формату 

```
<deviceAddress>:<clientId>
```


## Формирование заголовков 

```
[{
    name: 'X-Client-Token',
    value: <token>
}]
```


# Запросы к Datastore

## Запрос истории сообщений

Meтод: `GET`

#### GET параметры

| Параметр   | Описание                                                        |
|------------|-----------------------------------------------------------------|
| start      | Время отправки самого старого из загруженных сообщений          |
| count      | Максимальное количество сообщений, которое требуется подгрузить |
| libVersion | Версия приложения                                               |

#### Response

В случае отсутствия истории собщений для клиента будет получен статус-код ответа 404. При наличии истории ответ будет содержать массив сообщений.

```
[
    {
        id,
        providerId,
        threadId,
        client: {
            id,
            externalClientId,
            address,
            blocked,
            blockRequested
            banReason
        },
        receivedDate,
        channel: {
            id,
            address,
            channel: {
                id,
                channelType,
                appMarker,
                authorized
            }
        },
        read,
        pinned,
        text,
        attachments,
        quotes,
        type
    }    
]
```

| Параметр                      | Тип    | Описание                                          |  
|-------------------------------|--------|---------------------------------------------------|
| `id`                          | number | Идентификатор сообщения                           |
| `providerId`                  | string | Идентификатор сообщения на платформе (deprecated) |
| `threadId`                    | number | Идентификатор треда                               |
| `client.id`                   | number | Идентификатор клиента в системе                   |
| `client.externalClientId`     | number | Внешний интеграционный идентификатор клиента      |
| `client.address`              | string | Идентификатор устройства клиента                  |
| `client.blocked`              | bool   | Клиент заблокирован                               |
| `client.blockRequested`       | bool   | Оператор запросил блокировку клиента              |
| `client.banReason`            | string | Причина блокировки клиента                        |
| `receivedDate`                | string | Время отправки сообщения                          |
| `channel.id`                  | number | Идентификатор клиентского канала                  |
| `channel.address`             | string | Идентификатор устройства клиента                  |
| `channel.channel.id`          | number | Идентификатор канала                              |
| `channel.channel.channelType` | string | Тип канала                                        |
| `channel.channel.appMarker`   | string | Идентификатор приложения                          |
| `channel.channel.authorized`  | bool   | Авторизованный чат                                |
| `read`                        | bool   | Сообщение прочитано                               |
| `pinned`                      | bool   | Сообщение закреплено оператором                   |
| `type`                        | string | Тип сообщения                                     |


## Загрузка файла в хранилище

Meтод: `PUT`

#### Form data

| Параметр   | Описание          |
|------------|-------------------|
| file       | Отправляемый файл |

#### Response

```
{
    result,
    optional: {
        name,
        type,
        size
    }
}
```

| Параметр        | Тип    | Описание                           |  
|-----------------|--------|------------------------------------|
| `result`        | string | Идентификатор вложения в Datastore | 
| `optional.name` | string | Оригинальное название файла        | 
| `optional.type` | string | MIME-тип файла                     | 
| `optional.size` | string | Размер файла в байтах              | 
