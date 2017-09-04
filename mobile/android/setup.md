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

### **Шаг 3: Дайте необходимые права для приложения**
Для корректной работы приложения необходимо активировать настройку `Location` в настройках вашего приложения в разделе `permissions`.
B включить режим `High accuracy` в настройках местоположения.

