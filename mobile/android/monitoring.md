# Запуск и остановка мониторинга.
---
Для начала мониторинга ваших мобильных ресурсов необходимо выполнить пару шагов.

## **Шаг 1: Создайте водителя**
Для начала отслеживания нужно создать объект Driver. Вы можете создать его двумя путями, через API или через SDK.

### Через API
{% method %}
Для этого нужно создать объект Driver ([ссылка как это сделать](/api/objects/driver.md#driver-create)). И затем подключить его в SDK по его id.

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

### Через SDK
{% method %}
Для этого нужно передать объект с заполненными параметрами в метод `getOrCreateDriver`.

> Заметка.
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

## **Шаг 2: Запустите мониторинг**
{% method %}
После создания или получения ранее созданного объекта водителя можно запустить мониторинг. Для этого нужно вызвать метод `startTracking`.

{% sample lang="java" %}
```java
mTheTrack.startTracking(new ThetrackCallback<Void>() {
    @Override
    public void onSuccess(Void result) {
        String msg = "Мониторинг запущен";
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка запуска мониторинга: " + throwable;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }
});
```
{% endmethod %}

## **Шаг 3 (Дополнительный): Остановите мониторинг** {#android-stop-monitoring}
{% method %}
Если логика работы вашего приложение требует мониторить ресурсы не постоянно, то вы можете остановить мониторинг с помощью метода `stopTracking`.

> Заметка
> Остановка мониторинга не завершает и не отменяет текущую активную задачу. Для этого необходимо самостоятельно вызвать соответствующие методы после остановки мониторинга в методе колбэка onSuccess(). Подробнее о методах остановки задач смотрите в [руководстве по работе с задачами](/mobile/android/tasks_flow.md).

{% sample lang="java" %}
```java
mTheTrack.stopTracking(new ThetrackCallback<Void>() {
    @Override
    public void onSuccess(Void result) {
        String msg = "Мониторинг остановлен";
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка остановки мониторинга: " + throwable;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }
});
```
{% endmethod %}

