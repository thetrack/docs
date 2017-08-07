# Задачи \(Tasks\)
---
**Задача** - это сущность которая описывает действие совершаемое исполнителем. Каждое действие выполняемое исполнителем может быть представлено как задача. Например приложение для доставки может отслеживать получения, доставки или возвраты. А приложение для обслуживания клиентов посещения, оплату или встречи. В нашем случае мы создаем задачу с действием **deleivery** и местом назначения где клиент ожидает заказ.

## Поля {#fields}
| Поле          | Описание      |
| ------------- | ------------- |
|**id** <br/> *String*|Идентификатор задачи|
|**action** <br/> *String*|Действие. Возможные варианты: **task**, **pickup**, **delivery**, **visit**. По умолчанию **task**|
|**status** <br/> *String*|Текущий статус задачи|
|**progress** <br/> *String*|Текущий прогресс выполнения задачи|
|**start_location** <br/> *Json*|Местоположение исполнителя в момент начала задачи|
|**completion_location** <br/> *Json*|Местоположение водителя в момент окончания задачи|
|**cancellation_location** <br/> *Json*|Местоположение водителя в момент отмены задачи|
|**start_time** <br/> *String ISO8601 Datetime*|Время начала задачи|
|**completion_time** <br/> *String ISO8601 Datetime*|Время завершения задачи|
|**cancellation_time** <br/> *String ISO8601 Datetime*|Время отмены задачи|
|**location** <br/> *Json*|Место назначение задачи|
|**location_id** <br/> *String*|Id объекта местоназначения|
|**eta** <br/> *String ISO8601 Datetime*|Ожидаемое время прибытия исполнителя в место назначения задачи|
|**initial_eta** <br/> *String ISO8601 Datetime*|Ожидаемое время прибытия исполнителя в место назначения задачи вычисленное в начале задачи|
|**commited_eta** <br/> *String ISO8601 Datetime*|Список активный задач|
|**track** <br/> *GeoJson*|Трек пройденный исполнителем по этой задачи. Возвращает GeoJson типа LineString c списком гео точек.|
|**lookup_id** <br/> *String*|Уникальный идентификатор, который можно добавить в информацию о задачи. Вы можете записать сюда свой внутренний идентификатор|
|**driver_id** <br/> *String*|Id исполнителя задачи|
|**tracking_url** <br/> *String*|Короткая ссылка на браузерную версию карты с отслеживанием текущей задачи.|
## Поле action {#task-action}
## Поле status {#task-status}
## Поле progress {#task-progress}

{% method -%}
## Создание исполнителя {#driver-create}
Создает новый объект исполнителя.
### HTTP-запрос
POST https://api.thetrack.io/v1/drivers/
### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**name** <br/> *string* _Необязательный_|Имя исполнителя или название устройства|
|**phone** <br/> *string* _Необязательный_|Номер телефона в формате **E164**|
|**photo** <br/> *string* _Необязательный_|Ссылка на фото или иконку исполнителя|
|**vehicle_type** <br/> *string* _Необязательный_| Тип транспортного средства по умолчанию. Варианты: **car**, **transit**|
|**lookup_id** <br/> *string* _Необязательный_|Уникальный идентификатор, который можно добавить в информацию о водителе. Вы можете записать сюда свой внутрениий идентификатор|
### Возвращает
API возвращает объект исполнителя с его идентификатором. Этот идентификатор может использоваться для извлечения этого же объекта водителя в будущем.
```javascript
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
    "lookup_id": "your_internal_id"
}

```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/drivers/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/drivers/", json=params, headers=headers)
```
{% endmethod %}

