# Запуск отслеживания
---
Для начала мониторинга ваших ресурсов нам необходимо выполнить несколько шагов


### **Шаг 1: Создать водителя**
Для начала отслеживания нужно создать объект Driver. Вы можете создать его двумя путями, через API  или через SDK. 

{% method %}
#### Через API
Для этого нужно создать объект Driver [ссылка как это сделать](/api/objects/driver.md#driver-create). И затем подключить его в SDK по его id.
{% sample lang="java" %}
```java
mTheTrack.getDriver(DRIVER_ID, new ThetrackCallback<DriverModel>() {
    @Override
    public void onSuccess(@NonNull DriverModel result) {
        String msg = "Водитель получен: " + result.name;
        Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка получения водителя: " + throwable;
        Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
    }
});
```
{% endmethod %}

{% method %}
#### Через SDK
Для этого нужно передать объект с заполненными параметрами в метод `getOrCreateDriver`.

> Если еще раз попытаться создать объект Driver с одним и тем же `LookupID` то повторно объект создан не будет, а будет получен ранее созданный объект с таким же `LookupID`.

{% sample lang="java" %}
```java
DriverParams driverParams = new DriverParams.DriverParamsBuilder()
    .setName("Сусанин Иван")
    .setPhone("+79999999")
    .setLookupID("INTERNAL_ID")
    .create();

mTheTrack.getOrCreateDriver(driverParams, new ThetrackCallback<DriverModel>() {
    @Override
    public void onSuccess(@NonNull DriverModel result) {
        String msg = "Водитель создан: " + result.name;
        Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка создания водителя: " + throwable;
        Toast.makeText(this, msg, Toast.LENGTH_SHORT).show();
    }
});
```
{% endmethod %}

{% method %}
### **Шаг 2: Запустить трекинг на мобильном устройстве**
После создания или получения ранее созданного объекта водителя мы можем запустить отслеживание. Для этого нужно вызвать метод `startTracking`.
{% sample lang="java" %}
```java
mTheTrack.startTracking(new ThetrackCallback<Void>() {
    @Override
    public void onSuccess(Void result) {
        String msg = "Отслеживание запущенно";
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка пуска: " + throwable;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }
});
```
{% endmethod %}
