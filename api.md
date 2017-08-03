# Базовая интеграция c API

Первым шагом в серверной интеграции является создание объектов TheTrack, которые соответствуют вашим задачам. В этом руководстве мы создадим водителя, который будет осуществлять доставку для клиента.

Чтобы использовать примеры кода в руководстве, вам потребуется информация о секретном ключе и при необходимости, о дополнительных библиотеках. Если вы еще не знакомы с этой информацией, ознакомьтесь с руководством по началу работы, которое позволит понять аутентификацию и дополнительные библиотеки.



### **Шаг 1: Создание исполнителя \(Driver\)**

---

**Исполнитель** - это лицо, намеревающееся совершить доставку/прием или выполнение услуги. Вам требуется сделать следующий API вызов, чтобы создать водителя с именем водителя ‘name’ и типом транспортного средства ‘vehicle\_type’. Водителей можно также закрепить за парками.

```bash
curl https://api.thetrack.io/v1/drivers/ \
   -H "Authorization: token <your_secret_key>" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

API возвращает объект водителя с его идентификатором. Этот идентификатор может использоваться для извлечения этого же объекта водителя в будущем. Вам потребуется сохранить этот идентификатор в вашей базе данных, чтобы использовать его для последующих вызовов.

```js
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

### **Шаг 2: Создание задачи \(Task\)**

Каждое действие выполняемое пользователем может быть представлено как задача. Например приложение для доставки может отслеживать получения, доставки или возвраты. А приложение для обслуживания клиентов посещения, оплату или встречи.

```bash
curl https://api.thetrack.io/v1/tasks/ \
   -H "Authorization: token <your_secret_key>" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

Также можно использовать необязательное поле **committed\_eta**, определяющее установленные для задачи обязательства. Это поле используется для измерения соблюдения сроков.

```js
{
    "id": "a6085218-cf32-4d4e-9649-c96715ce4ef5",
    "status": "pending",
    "action": "delivery",
    "start_location": null,
    "completion_location": null,
    "cancellation_location": null,
    "start_time": null,
    "completion_time": null,
    "cancellation_time": null,
    "location": {
        "id": "93d38517-1b7f-4c02-b23e-b07c6d07a885",
        "address": "ш. Ярославское 22к3 кв67",
        "landmark": "",
        "point": {
            "type": "Point",
            "coordinates": [
                55.856652,
                37.685938
            ]
        }
    },
    "location_id": "93d38517-1b7f-4c02-b23e-b07c6d07a885",
    "eta": null,
    "initial_eta": null,
    "commited_eta": null,
    "track": null,
    "lookup_id": "123",
    "driver_id": null,
    "tracking_url": "http://eta.st/rasFkN"
}
```

### **Шаг 3: Назначение задачи исполнителю \(**assign\_tasks**\)**

После того как будет создана задача её можно будет назначить конкретному исполнителю.

```bash
curl https://api.thetrack.io/v1/drivers/<DRIVER_ID>/assign_tasks/ \
   -H "Authorization: token <your_secret_key>" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

```js
{
    "id": "875f2517-def3-4951-be01-3402eac6ea4d",
    "active_tasks": [
        {
            "id": "a6085218-cf32-4d4e-9649-c96715ce4ef5",
            "status": "assigned",
            "action": "delivery",
            "location": {
                "id": "dcf61eb5-fa1b-44c9-be42-dc4ffc1c651b",
                "address": "ш. Ярославское 22к3 кв67",
                "landmark": "",
                "point": {
                    "type": "Point",
                    "coordinates": [
                        55.856652,
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
    "phone": "+79268254144",
    "vehicle_type": "car",
    "location": {
        "type": "Point",
        "coordinates": []
    },
    "lookup_id": "1232"
}
```





