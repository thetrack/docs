# Работа с задачами
После запуска мониторинга, TheTrack SDK автоматически запрашивает очередь активных задач исполнителя и запускает последовательное их выполнение. Завершение или отмена задачи должна быть подтверждена исполнителем вручную. Для этого нужно вызвать методы SDK `completeCurrentTask` или `cancelCurrentTask`.

## Получение очереди задач.
{% method %}
Для отображения очереди задач, или для получения текущей активной задачи нужно использовать методом `getTasks`.

{% sample lang="java" %}
```java
mTheTrack.getTasks(new ThetrackCallback<List<TaskModel>>() {
    @Override
    public void onSuccess(@NonNull List<TaskModel> result) {
        String msg = "Текущая активная задача: " + result.get(0).id;
        Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_SHORT).show();
    }

    @Override
    public void onError(@NonNull Throwable throwable) {
        String msg = "Ошибка получения очереди задач" + throwable;
            Toast.makeText(getApplicationContext(), msg, Toast.LENGTH_SHORT).show();
        }
});
```
{% endmethod %}

{% method %}
## Завершение активной задачи
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
## Отмена активной задачи
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