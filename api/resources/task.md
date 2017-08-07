# Задачи \(Tasks\)
---
**Задача** - это сущность которая описывает действие совершаемое исполнителем. 

Каждое действие выполняемое исполнителем может быть представлено как задача. Например приложение для доставки может отслеживать получения, доставки или возвраты. А приложение для обслуживания клиентов посещения, оплату или встречи.


## Поля {#fields}
| Поле          | Описание      |
| ------------- | ------------- |
|**id** <br/> *String*|Идентификатор задачи|
|**action** <br/> *String*|Действие. Возможные варианты: **task**, **pickup**, **delivery**, **visit**. |
|**status** <br/> *String*|Текущий статус задачи. Варианты: **pending**, **assigned**, **in_queue**, **started**, **completed**, **canceled**, **suspended**|
|**progress** <br/> *String*|Текущий прогресс выполнения задачи. Варианты: **pending**, **on_the_way**, **arriving**, **arrived**|
|**start_location** <br/> *Json*|Местоположение исполнителя в момент начала задачи. Возвращает объект Location|
|**completion_location** <br/> *Json*|Местоположение водителя в момент окончания задачи. Возвращает объект Location|
|**cancellation_location** <br/> *Json*|Местоположение водителя в момент отмены задачи. Возвращает объект Location|
|**start_time** <br/> *String ISO8601 Datetime*|Время начала задачи|
|**completion_time** <br/> *String ISO8601 Datetime*|Время завершения задачи|
|**cancellation_time** <br/> *String ISO8601 Datetime*|Время отмены задачи|
|**location** <br/> *Json*|Место назначение задачи. Возвращает объект Location|
|**location_id** <br/> *String*|Id объекта местоназначения|
|**eta** <br/> *String ISO8601 Datetime*|Ожидаемое время прибытия исполнителя в место назначения задачи|
|**initial_eta** <br/> *String ISO8601 Datetime*|Ожидаемое время прибытия исполнителя в место назначения задачи вычисленное в начале задачи|
|**commited_eta** <br/> *String ISO8601 Datetime*|Обещанное время выполнения задачи. Это поле используется для контроля первоначально обещанного время прибытия|
|**track** <br/> *GeoJson*|Трек пройденный исполнителем по этой задачи. Возвращает GeoJson типа LineString c списком гео точек.|
|**distance** <br/> *Integer*|Расстояние пройденное исполнителем по задачи в метрах|
|**lookup_id** <br/> *String*|Уникальный идентификатор, который можно добавить в информацию о задачи. Вы можете записать сюда свой внутренний идентификатор|
|**driver_id** <br/> *String*|Id исполнителя задачи|
|**tracking_url** <br/> *String*|Короткая ссылка на браузерную версию карты с отслеживанием текущей задачи.|

{% method -%}
## Создание задачи {#task-create}
Создает новый объект задачи.
### HTTP-запрос
POST https://api.thetrack.io/v1/tasks/
### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**action** <br/> *string* _Необязательно_|Действие. По умолчанию **task**|
|**location** <br/> *Json* _Необязательно_|Местоназначение. Формат такой же как и при создании объекта [Location](/api/resources/location.md)|
|**location_id** <br/> *string* _Необязательный_|ID объекта Location. Можно указать информацию через поле location или создать объект [Location](/api/resources/location.md) заранее и передать его ID в это поле.|
|**commited_eta** <br/> *String ISO8601 Datetime* _Необязательно_|Обещанное клиенту время прибытия|
|**lookup_id** <br/> *string* _Необязательно_|Уникальный идентификатор, который можно добавить в информацию о задачи. Вы можете записать сюда свой внутренний идентификатор|

> Внимание!!!
> Одновременно можно передать либо поле location либо location_id.

### Возвращает
API возвращает объект задачи с его идентификатором. Этот идентификатор может использоваться для извлечения этого же объекта в будущем.
```javascript
{
    "id": "59b5ac60-0c17-4010-85c1-204dd8f44eac",
    "driver_id": null,
    "status": "pending",
    "progress": "pending",
    "action": "delivery",
    "location": {
        "id": "27510977-acd1-4ab6-ac32-a6d2b073ce0e",
        "address": "ш. Волоколамское 33",
        "landmark": "",
        "point": null
    },
    "location_id": "27510977-acd1-4ab6-ac32-a6d2b073ce0e",
    "start_location": null,
    "completion_location": null,
    "cancellation_location": null,
    "start_time": null,
    "completion_time": null,
    "cancellation_time": null,
    "eta": null,
    "initial_eta": null,
    "commited_eta": null,
    "track": null,
    "distance": null,
    "lookup_id": "1233",
    "tracking_url": "http://eta.st/ShaUJe"
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/tasks/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/tasks/", json=params, headers=headers)
```
{% endmethod %}

{% method -%}
## Получение задачи {#task-retrieve}
Получает ранее созданный объект задачи.
### HTTP-запрос
GET https://api.thetrack.io/v1/tasks/TASK_ID/
### Возвращает
API возвращает ранее созданный объект.
```javascript
{
    "id": "59b5ac60-0c17-4010-85c1-204dd8f44eac",
    "driver_id": null,
    "status": "pending",
    "progress": "pending",
    "action": "delivery",
    "location": {
        "id": "27510977-acd1-4ab6-ac32-a6d2b073ce0e",
        "address": "ш. Волоколамское 33",
        "landmark": "",
        "point": null
    },
    "location_id": "27510977-acd1-4ab6-ac32-a6d2b073ce0e",
    "start_location": null,
    "completion_location": null,
    "cancellation_location": null,
    "start_time": null,
    "completion_time": null,
    "cancellation_time": null,
    "eta": null,
    "initial_eta": null,
    "commited_eta": null,
    "track": null,
    "distance": null,
    "lookup_id": "1233",
    "tracking_url": "http://eta.st/ShaUJe"
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/tasks/TASK_ID/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json"
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.get("https://api.thetrack.io/v1/tasks/TASK_ID/", headers=headers)
```
{% endmethod %}

{% method -%}
## Получение списка задач {#task-list}
Получает список задач.
### HTTP-запрос
GET https://api.thetrack.io/v1/tasks/
### Возвращает
API возвращает ранее созданные объекты задач. Использует [Пагинатор](/api/README.md#api-pagination)
```javascript
{
    "count": 100,
    "next": "https://api.thetrack.io/v1/tasks/?page=3",
    "previous": "https://api.thetrack.io/v1/tasks/?page=1",
    "results": [
        {
            "id": "5958f67b-6a36-44f1-acf1-027ce93cbb8e",
            "driver_id": "a0cd9595-4ba8-45d2-b1d6-3e49ccf50c69",
            "status": "started",
            "progress": "on_the_way",
            "action": "task",
            "location": {
                "id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
                "address": "Mail.ru",
                "landmark": "",
                "point": {
                    "type": "Point",
                    "coordinates": [
                        37.53752588703264,
                        55.79713792800458
                    ]
                }
            },
            "location_id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
            "start_location": null,
            "completion_location": null,
            "cancellation_location": null,
            "start_time": "2017-08-01T17:57:53.875350Z",
            "completion_time": null,
            "cancellation_time": null,
            "eta": "2017-08-01T19:06:05.022000Z",
            "initial_eta": "2017-08-01T19:06:05.022000Z",
            "commited_eta": "2017-08-01T19:06:05.022000Z",
            "track": null,
            "distance": null,
            "lookup_id": "",
            "tracking_url": "http://eta.st/A8MEQc"
        },
        {
            "id": "d06da4f4-1c19-4d68-9ef6-bc16de5eedbf",
            "driver_id": "a0cd9595-4ba8-45d2-b1d6-3e49ccf50c69",
            "status": "assigned",
            "progress": "pending",
            "action": "task",
            "location": {
                "id": "ab39333f-11f8-43a4-8b0c-ac2b14a54e6c",
                "address": "Ярославское шоссе 22к3",
                "landmark": "Дом",
                "point": {
                    "type": "Point",
                    "coordinates": [
                        37.685916418553106,
                        55.856715713580826
                    ]
                }
            },
            "location_id": "ab39333f-11f8-43a4-8b0c-ac2b14a54e6c",
            "start_location": null,
            "completion_location": null,
            "cancellation_location": null,
            "start_time": null,
            "completion_time": null,
            "cancellation_time": null,
            "eta": "2017-08-01T19:31:33.022000Z",
            "initial_eta": "2017-08-01T19:31:33.022000Z",
            "commited_eta": "2017-08-01T19:31:33.022000Z",
            "track": null,
            "distance": null,
            "lookup_id": "",
            "tracking_url": "http://eta.st/MiA7kD"
        },
        ...
    ]
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/tasks/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json"
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.get("https://api.thetrack.io/v1/tasks/", headers=headers)
```
{% endmethod %}

{% method -%}
## Завершение задачи {#task-complete}
Завершает задачу в указанном месте и времени.
### HTTP-запрос
POST https://api.thetrack.io/v1/tasks/TASK_ID/complete/
### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**completion_location** <br/> *Json* _Необязательно_|Место завершения задачи. Формат такой же как и при создании объекта [Location](/api/resources/location.md).|
|**completion_time** <br/> *String ISO8601 Datetime*|Время завершения задачи. Если поле не указано то по умолчанию текущее время|

### Возвращает
Возвращает завершенный объект задачи.
```javascript
{
    "id": "5958f67b-6a36-44f1-acf1-027ce93cbb8e",
    "driver_id": "a0cd9595-4ba8-45d2-b1d6-3e49ccf50c69",
    "status": "completed",
    "progress": "on_the_way",
    "action": "task",
    "location": {
        "id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
        "address": "Mail.ru",
        "landmark": "",
        "point": {
            "type": "Point",
            "coordinates": [
                37.53752588703264,
                55.79713792800458
            ]
        }
    },
    "location_id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
    "start_location": null,
    "completion_location": null,
    "cancellation_location": null,
    "start_time": "2017-08-01T17:57:53.875350Z",
    "completion_time": "2017-08-07T12:12:07.939057Z",
    "cancellation_time": null,
    "eta": "2017-08-01T19:06:05.022000Z",
    "initial_eta": "2017-08-01T19:06:05.022000Z",
    "commited_eta": "2017-08-01T19:06:05.022000Z",
    "track": null,
    "distance": null,
    "lookup_id": "",
    "tracking_url": "http://eta.st/A8MEQc"
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/tasks/TASK_ID/complete/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/tasks/TASK_ID/complete/", json=params, headers=headers)
```
{% endmethod %}

{% method -%}
## Отмена задачи {#task-cancel}
Отменяет задачу в указанном месте и времени.
### HTTP-запрос
POST https://api.thetrack.io/v1/tasks/TASK_ID/cancel/
### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**cancellation_location** <br/> *Json* _Необязательно_|Место отмены задачи. Формат такой же как и при создании объекта [Location](/api/resources/location.md).|
|**concellation_time** <br/> *String ISO8601 Datetime*|Время отмены задачи. Если поле не указано то по умолчанию текущее время|

### Возвращает
Возвращает завершенный объект задачи.
```javascript
{
    "id": "5958f67b-6a36-44f1-acf1-027ce93cbb8e",
    "driver_id": "a0cd9595-4ba8-45d2-b1d6-3e49ccf50c69",
    "status": "canceled",
    "progress": "on_the_way",
    "action": "task",
    "location": {
        "id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
        "address": "Mail.ru",
        "landmark": "",
        "point": {
            "type": "Point",
            "coordinates": [
                37.53752588703264,
                55.79713792800458
            ]
        }
    },
    "location_id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
    "start_location": null,
    "completion_location": null,
    "cancellation_location": null,
    "start_time": "2017-08-01T17:57:53.875350Z",
    "completion_time": null,
    "cancellation_time": "2017-08-07T12:12:07.939057Z",
    "eta": "2017-08-01T19:06:05.022000Z",
    "initial_eta": "2017-08-01T19:06:05.022000Z",
    "commited_eta": "2017-08-01T19:06:05.022000Z",
    "track": null,
    "distance": null,
    "lookup_id": "",
    "tracking_url": "http://eta.st/A8MEQc"
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/tasks/TASK_ID/cancel/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/tasks/TASK_ID/cancel/", json=params, headers=headers)
```
{% endmethod %}