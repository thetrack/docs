# Исполнитель \(Driver\)
---
**Исполнитель** - это лицо или устройство которое нам необходимо отслеживать. В API исполнитель называется Driver.
## Поля
| Поле          | Описание      |
| ------------- | ------------- |
|**id** <br/> *string*|Идентификатор исполнителя|
|**name** <br/> *string*|Имя исполнителя или название устройства|
|**phone** <br/> *string*|Номер телефона в формате **E164**|
|**photo** <br/> *string*|Ссылка на фото или иконку исполнителя|
|**location** <br/> *GeoJson*|Текущее местоположение водителя|
|**vehicle_type** <br/> *string*| Тип транспортного средства по умолчанию. Возможные варианты: **car** - авто транспорт, **transit** - пеший исполнитель|
|**lookup_id** <br/> *string*|Уникальный идентификатор, который можно добавить в информацию о водителе. Вы можете записать сюда свой внутрениий идентификатор|
|**active_tasks** <br/> *Json*|Список активный задач|
|**created** <br/> *String ISO8601 Datetime*|Дата создания объекта|

{% method -%}
## Создание исполнителя {#driver-create}
Создает новый объект исполнителя.
## HTTP-запрос
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

{% method -%}
## Получение исполнителя {#driver-retrieve}
Получает ранее созданный объект исполнителя.
## HTTP-запрос
GET https://api.thetrack.io/v1/drivers/DRIVER_ID/
### Возвращает
API возвращает ранее созданный объект исполнителя.
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
$ curl https://api.thetrack.io/v1/drivers/875f2517-def3-4951-be01-3402eac6ea4d/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json"
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.get("https://api.thetrack.io/v1/drivers/875f2517-def3-4951-be01-3402eac6ea4d/", headers=headers)
```
{% endmethod %}

{% method -%}
## Получение списка всех исполнителей {#driver-list}
Получает список всех доступных исполнителей.
## HTTP-запрос
GET https://api.thetrack.io/v1/drivers/
### Возвращает
API возвращает ранее созданные объекты исполнителей. За один раз выводится по 50 записей. Для запроса следуйщих записей необходимо добавить номер страницы в параметры GET запроса вида `?page=N`. Поле `count` означает общее кол-во записей.
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

{% method -%}
## Привязка задач к исполнителю {#driver-assign-task}
Привязывает задачи к водителю.

## HTTP-запрос
POST https://api.thetrack.io/v1/drivers/DRIVER_ID/assign_tasks/
```javascript
// Пример тела сообщения
{
    "task_ids": ["72118cb0-7583-4829-936b-71c5bf4c75e3", "65555ffa-06b6-47ee-9b3c-943a03833090"]
}
```

### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**task_ids** <br/> *список* <br/> _Обязательный_|Список идентификаторов задач|

### Возвращает
API возвращает объект исполнителя с заполненым полем active_tasks.
```javascript
{
	"id": "875f2517-def3-4951-be01-3402eac6ea4d",
	"active_tasks": [{
			"id": "72118cb0-7583-4829-936b-71c5bf4c75e3",
			"status": "assigned",
			"action": "task",
			"location": {
				"id": "1a6502af-cbb2-4dfe-a5e9-e1bd2c76959c",
				"address": "г. Москва. ул. Кунцевская 12",
				"landmark": "",
				"point": {
					"type": "Point",
					"coordinates": [
						37.53752588703264,
						55.79713792800458
					]
				}
			},
			"lookup_id": "",
			"tracking_url": "http://eta.st/idjNbt"
		},
		{
			"id": "65555ffa-06b6-47ee-9b3c-943a03833090",
			"status": "assigned",
			"action": "delivery",
			"location": {
				"id": "dcf61eb5-fa1b-44c9-be42-dc4ffc1c651b",
				"address": "г. Москва. ш. Варшавское 44-3",
				"landmark": "",
				"point": {
					"type": "Point",
					"coordinates": [
						55.657652,
						37.685938
					]
				}
			},
			"lookup_id": "123",
			"tracking_url": "http://eta.st/6HRKV3"
		}
	],
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
$ curl https://api.thetrack.io/v1/drivers/assign_tasks/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/drivers/assign_tasks/", json=params, headers=headers)
```
{% endmethod %}
