# Работа с задачами
После запуска мониторинга, TheTrack SDK автоматически запрашивает очередь активных задач исполнителя и запускает последовательное их выполнение. Завершение или отмена задачи должна быть подтверждена исполнителем вручную. Для этого нужно вызвать методы SDK `completeCurrentTask` или `cancelCurrentTask`.

{% method %}
### Завершение активной задачи
После того как исполнитель завершил задачу необходимо вызвать метод `completeCurrentTask`. После чего текущая активная задача будет завершена и автоматически запуститься следующая в очереди задача.

{% sample lang="java" %}
```java
mTheTrack.completeCurrentTask(new ThetrackCallback<TaskModel>() {
    @Override
    public void onSuccess(@NonNull TaskModel result) {
        String msg = "Текущая задача завершена" + result.id;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка завершения задачи: " + throwable;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }
});
```
{% endmethod %}

{% method %}
### Отмена активной задачи
Если по каким либо причинам исполнитель не может продолжать выполнение текущей задачи нужно вызвать метод `cancelCurrentTask`. После чего будет автоматически запущена следующая задача в очереди.

> Заметка
> Если нужно полностью остановить выполнение всех задач, то перед отменой текущей задачи нужно полностью остановить мониторинг (см. [запуск и остановка мониторинга](/mobile/android/monitoring.md#android-stop-monitoring)).

{% sample lang="java" %}
```java
mTheTrack.cancelCurrentTask(new ThetrackCallback<TaskModel>() {
    @Override
    public void onSuccess(@NonNull TaskModel result) {
        String msg = "Текущая задача отменена" + result.id;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка отмены задачи: " + throwable;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_LONG).show();
    }
});
```
{% endmethod %}