# Базовая интеграция c API

Первым шагом в серверной интеграции является создание объектов TheTrack, которые соответствуют вашим задачам. В этом руководстве мы создадим курьера, который будет осуществлять доставку для клиента.

> **Внимание!!!**
> Чтобы использовать примеры в руководстве, вам потребуется секретный ключ которой вы получите после регистрации.

### **Шаг 1: Создание объекта Driver**
---

**[Driver](/api/objects/driver.md)** - это лицо или устройство которое нам необходимо отслеживать. В нашем случае мы создадим курьера с автомобилем, именем Иван Диктирёв и произвольным номером телефона.

```bash
curl https://api.thetrack.io/v1/drivers/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

API возвращает объект исполнителя с его идентификатором. Этот идентификатор может использоваться для извлечения этого же объекта в будущем. Вам потребуется сохранить этот идентификатор в вашей базе данных, чтобы использовать его для последующих вызовов.

```js
// @body.json
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

### **Шаг 2: Создание объекта Task**

Каждое действие выполняемое исполнителем может быть представлено как задача ([Task](/api/objects/task.md)). Например приложение для доставки может отслеживать получения, доставки или возвраты. А приложение для обслуживания клиентов посещения, оплату или встречи. В нашем случае мы создаем задачу с действием **deleivery** и местом назначения где клиент ожидает заказ от курьера.

```bash
curl https://api.thetrack.io/v1/tasks/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

```js
{
    "action": "delivery",
    "location": {
        "address": "ш. Ярославское 13"
    },
    "lookup_id": "1"
}
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
        "address": "ш. Ярославское 22",
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

После того как будет создана задача её можно будет [назначить](/api/objects/driver.md#assign-task) конкретному исполнителю. Это даст нам возможность отслеживать передвижение курьера по конкретной задачи.

```bash
curl https://api.thetrack.io/v1/drivers/<DRIVER_ID>/assign_tasks/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

В ответ мы получим объект Driver с заполненным полем active\_tasks. В этом поле находятся все задачи которые были назначены на исполнителя и которые он последовательно будет выполнять.

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



