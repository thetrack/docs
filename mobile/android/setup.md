# Установка
----
Для использования Thetrack в мобильном приложении необходимо подключить и настроить библиотеку **io.thetrack:sdk**

{% method %}
### **Шаг 1: Подключите библиотеку**
В файле `build.gradle` пропишите репозиторий и зависимость.

{% sample lang="java" %}
```java
repositories {
    maven { url 'https://repo.thetrack.io/repository/maven-releases/' }
}

dependencies {
    compile('io.thetrack:sdk:3.0.1:release@aar') {
        transitive = true;
    }
}
```
{% endmethod %}

{% method %}
### **Шаг 2: Настройте SDK**
После того как вы установили SDK необходимо его проинициализировать и настроить. В методе `OnCreate` вашего приложения выполните код как в примере.

> Для инициализации SDK вам понадобится публичный ключ который вы получите после регистрации

{% sample lang="java" %}
```java
TheTrack theTrack = TheTrack.getInstance(PUBLIC_KEY, getApplicationContext());
```
{% endmethod %}

{% method %}
### **Шаг 3: Дайте необходимые права для приложения**
Для корректной работы SDK нужны разрешения для `ACCESS_FINE_LOCATION`. В манифесте SDK они уже прописаны, поэтому дополнительно в манифесте вашего приложение ничего делать не нужно. Для Android SDK 23 и выше необходимо явно их запросить с помощью метода `requestPermissions`.

Также SDK требуется включенный режим `High accuracy` в настройках местоположения. Для более точного определение местоположения.

> Мы рекомендуем воспользоваться примером из [gist](https://gist.github.com/voron3x/7d6627f1e2017e72729edb18023fa1be "gist") для обработки исключений которые могут возникнуть в процессе запроса прав.

{% sample lang="java" %}
```java
theTrack.requestPermissions((Activity) this);
theTrack.requestLocationSettings((Activity) this);
```
{% endmethod %}
