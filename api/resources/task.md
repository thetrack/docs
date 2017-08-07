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
## Создание задачи {#teask-create}
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
## Получение списка всех исполнителей {#task-list}
Получает список всех задач.
### HTTP-запрос
GET https://api.thetrack.io/v1/tasks/
### Возвращает
API возвращает ранее созданные объекты задач. Использует [Пагинатор](/api/README.md#api-pagination)
```javascript
{
    "count": 94,
    "next": "http://localhost:8000/api/v1/drivers/?page=2",
    "previous": null,
    "results": [
        {
            "id": "875f2517-def3-4951-be01-3402eac6ea4d",
            "active_tasks": [],
            "name": "Иван Диктирёв",
            "photo": null,
            "phone": "+71234567890",
            "vehicle_type": "car",
            "location": {
                "type": "Point",
                "coordinates": []
            },
            "lookup_id": "1232",
            "created": "2017-08-03T14:14:12.992602Z"
        },
        {
            "id": "a0cd9595-4ba8-45d2-b1d6-3e49ccf50c69",
            "active_tasks": [],
            "name": "Василий Лобанов",
            "photo": null,
            "phone": "+71234567890",
            "vehicle_type": "car",
            "location": {
                "type": "Point",
                "coordinates": [
                    37.58158653451538,
                    55.71143605680116
                ]
            },
            "lookup_id": "123",
            "created": "2017-07-28T10:25:14.912898Z"
        },
        ...
    ]
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/drivers/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json"
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.get("https://api.thetrack.io/v1/drivers/", headers=headers)
```
{% endmethod %}