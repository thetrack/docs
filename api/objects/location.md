# Местонахождение \(Location\)
---
**Местонахождение** - Это объект описывающий адрес или географические координаты точки. Местонахождения используется в API для описания каких либо объектов находящихся в пространстве. Например Location описывает место в которое осуществляется доставка для клиента.

## Поля {#fields}
| Поле          | Описание      |
| ------------- | ------------- |
|**id** <br/> *string*|Идентификатор объекта|
|**address** <br/> *string*|Адрес места|
|**landmark** <br/> *string*|Ориентир|
|**point** <br/> *Geоjson*|Координаты точки в формате GeoJson|
|**created** <br/> *String ISO8601 Datetime*|Дата создания объекта|

{% method -%}
## Создание местонахождения {#location-create}
Создает новый объект местонахождения.

### HTTP-запрос
POST https://api.thetrack.io/v1/locations/

### Аргументы
| Имя           | Описание      |
| ------------- | ------------- |
|**address** <br/> *string* _Необязательно_|Адрес места в произвольном формате|
|**landmark** <br/> *string* _Необязательно_|Ориентир, произвольное описание места|
|**point** <br/> *string* _Необязательно_|Координаты точки в формате GeoJson|

> **Внимание!!!**
> Одновременно можно указать либо адрес либо координаты

> _Заметка_
> После создания объекта с адресом, автоматически будет заполнена поле point и наоборот. 

### Возвращает
API возвращает объект местонахождения с его идентификатором.
```javascript
{
    "id": "1323776e-48eb-453c-b499-b133139ff954",
    "address": "Ярославская улица, 14к2",
    "landmark": "",
    "point": null,
    "created": "2017-08-07T15:21:53.677696Z"
}
```
{% sample lang="curl" -%}
```bash
$ curl https://api.thetrack.io/v1/locations/ \
   -H "Authorization: token sk_token" \
   -H "Content-Type: application/json" \
   -X POST \
   -d @body.json
```

{% sample lang="python" -%}
```python
>>> import requests
>>> headers = {'Authorization': 'token sk_token'}
>>> r = requests.post("https://api.thetrack.io/v1/locations/", json=params, headers=headers)
```
{% endmethod %}