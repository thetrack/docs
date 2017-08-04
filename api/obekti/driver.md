# Исполнитель \(Driver\)
---

## Поля
| Поле          | Описание      |
| ------------- | ------------- |
| **name** <br/> *string* | Имя исполнителя или идентификатор устройства |
| **phone** <br/> *string* | Номер телефона |
|**vehicle_type** <br/> *string*| Тип транспортного средства по умолчанию|

{% method -%}
## Install {#install}
The first thing is to get the GitBook API client.

{% sample lang="js" -%}
```bash
$ npm install gitbook-api
```

{% sample lang="go" -%}
```bash
$ go get github.com/GitbookIO/go-gitbook-api
```
{% endmethod %}