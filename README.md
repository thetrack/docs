# TheTrack.io
---

## Возможности
#### Отслеживание текущего местонахождения
* Позволит отслеживать на карте в режиме реального времени перемещение транспорта или сотрудников.
* Позволит всегда быть в курсе где конкретно находится ваш транспорт или сотрудник.

#### Отслеживание задач
* Позволит клиенту отслеживать исполнителя и его время прибытия в назначенное место c учетом пробок.
* Позволит диспетчерам планировать и формировать список задач, контролировать их статус выполнения и понимать когда и где освободится транспорт или сотрудник.

#### Назначение задачи ближайшему исполнителю
* Позволит увеличить производительность за счет выбора ближайшего исполнителя 
* Позволит сократить накладные расходы на выполнение задачи за счет сокращения расстояния и времени при исполнении задачи ближайшим из возможных.

#### Учет расходов по пройденному расстоянию и времени
* Позволит объективно оценить выполненную работу.
* Позволит контролировать выработку ваших сотрудников и транспорта.
* Позволит определить загрузку служб и прогнозировать их работу.

#### Оповещение о событиях на маршруте
* Позволит клиентам иметь полную информацию о статусе его заказа и времени его исполнения.
* Позволит диспетчерам контролировать ход исполнения задач.
* Позволит сотруднику своевременно информировать о происходящих на маршруте событиях.

## Что мы делаем
Мы упрощаем создание и использование функций отслеживания местоположения в режиме реального времени до нескольких простых вызовов API. Разработчики используют TheTrack для создания функций отслеживания местоположения, а не инфраструктуры.

## Для кого мы это делаем
Среди наших пользователей есть разработчики, для которых функции отслеживания местоположения являются:

* Классным дополнением, которое улучшает опыт использования их продукта.
* Неотъемлемой частью деятельности благодаря экономии финансов.
* Основной частью их продуктовой линейки, от которой зависит их бизнес.

## Как это работает

TheTrack интегрируется в два простых шага:

1. **Подключите SDK водителя в приложение водителя:** SDK собирает данные о местоположении с учетом оптимизации расхода аккумуляторов и привязки по времени. И отправляет на сервер TheTrack, где они проходят фильтрацию в режиме реального времени и используются с целью отслеживания в реальном времени, после чего сохраняются для последующей обработки и аналитики.
2. **С помощью REST API определите объекты которые вы хотите отслеживать:** TheTrack REST API обменивается данными с сервером вашего приложения для создания объектов для отслеживания.

| Объект | Описание |
| :--- | :--- |
| **Driver** | Определяет того кто будет осуществлять доставку товара или услуги и того кого в последствии мы будем отслеживать. |
| **Task** | Определяет доставляемый или принятый от клиента заказ. |
| **Location** | Место назначение заказа или место в котором должна быть выполнена услуга. |

## Как с нами связаться
[hello@thetrack.io](mailto:opoldushina@thetrack.io) - По вопросам сотрудничества

[support@thetrack.io](mailto:tkozhevnikov@thetrack.io) - По техническим вопросам и поддержки

