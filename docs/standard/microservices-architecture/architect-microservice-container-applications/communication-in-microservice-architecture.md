---
title: "Обмен данными в архитектуре микрослужбу"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Обмен данными в архитектурах микрослужбу архитектуры"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/18/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 8d38095a151b7568619b17340d768eff684d3271
ms.sourcegitcommit: c2e216692ef7576a213ae16af2377cd98d1a67fa
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/22/2017
---
# <a name="communication-in-a-microservice-architecture"></a>Обмен данными в архитектуре микрослужбу

Монолитные приложения, работающего в одном процессе компоненты вызывать друг с другом с помощью метода уровня языка или вызовы функций. Это может быть тесно связаны при создании объектов с кодом (например, `new ClassName()`), или можно вызывать несвязанной образом с помощью внедрения зависимости, ссылаясь на абстрактные классы, а не конкретный объект экземпляров. В любом случае объекты выполняются в одном процессе. Самая сложная задача при изменении монолитные приложения для приложения на основе микрослужбами заключается в изменении механизм обмена данными. Прямое преобразование из вызовов методов в процессе в вызовы RPC службы приведет к «многословных» и не эффективного взаимодействия, которая не будет выполняться в распределенных средах. Трудностей при проектировании распределенной системе должным образом достаточно хорошо известны это даже canon, известный как [fallacies распределенных вычислений](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing) , в которой перечислены предположений, которые разработчики часто при переходе от монолитные для распределенных разработок.

Нет, не одно из решений, но некоторые. Одно решение включает в себя изоляция максимально микрослужбами бизнеса. Затем используйте асинхронную связь между внутренней микрослужбами и замените детально взаимодействие, обычно внутри процесса связи между объектами, имеющими крупногранулированную связи. Это можно сделать, группируя вызовов и возвращая данные, объединяет результаты нескольких внутренних вызовов клиенту.

Приложения на основе микрослужбами является распределенных систем, работающих на несколько процессов или служб, обычно даже между несколькими серверами или узлов. Как правило, каждый экземпляр службы — это процесс. Таким образом службы должны взаимодействовать по протоколу межпроцессного взаимодействия, например, HTTP, AMQP или двоичный протокол, такой как TCP, в зависимости от характера каждой службы.

Сообщество микрослужбу способствует философии "[смарт-конечные точки и каналы ввода-вывода](http://simplicable.com/new/smart-endpoints-and-dumb-pipes).» Это слоган стимулирует макет, как связаны, как можно между микрослужбами и как целостного максимально в пределах одного микрослужбу. Как упоминалось ранее, собственные данные и логику домена, принадлежат каждого микрослужбу. Но микрослужбами, составление-готовое приложение обычно просто choreographed с помощью REST связи, а не сложных протоколов, таких как WS -\* и централизованное гибкие связи с событиями вместо бизнес процесс orchestrators.

Два часто используемых протоколов, запросов и ответов HTTP с ресурсом API-интерфейсы (при запросе большинство всех) и время упрощенных асинхронный обмен сообщениями при обмене данными через несколько микрослужбами. Это описано в следующих разделах более подробно.

## <a name="communication-types"></a>Типы взаимодействия

Клиента и службы могут взаимодействовать через различные виды взаимодействия, предназначенные для различных сценариев и цели каждого из них. Изначально этих типов сообщений могут быть классифицированы две оси.

Если протокол синхронный или асинхронный, является определение первой оси:

-   Синхронные протокол. Синхронные протокол HTTP не. Клиент отправляет запрос и ожидает ответа от службы. Независимо от выполнения кода клиента, может быть синхронным (поток заблокирован) или асинхронные (поток не заблокирован, и ответ в конечном счете достигнет обратный вызов). Здесь важно то, что протокол (HTTP/HTTPS) является синхронным и код клиента можно продолжить свою задачу, только при получении HTTP-ответа сервера.

-   Асинхронный протокол. Другие протоколы, например AMQP (протокол поддерживает несколько операционных систем и облачных средах) с помощью асинхронных сообщений. Отправитель Код или сообщение клиента обычно не ожидает ответа. Он просто отправляет сообщения в виде при отправке сообщения в очередь RabbitMQ или других брокер обмена сообщениями.

Если обмен данными имеет один получатель или нескольким получателям, является определение второй оси:

-   Один получатель. Каждый запрос должен обрабатываться ровно один получатель или службой. Примером этого является [команд](https://en.wikipedia.org/wiki/Command_pattern).

-   Нескольким получателям. Каждый запрос могут обрабатываться на ноль между несколькими получателями. Этот тип обмена данными должен выполняться асинхронно. Например, [публикации или подписки](https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) механизм, используемый в шаблонах, таких как [событиями архитектура](http://microservices.io/patterns/data/event-driven-architecture.html). Следующий пример основан на интерфейс или сообщения компонента broker событий шины при распространении обновлений данных между несколькими микрослужбами через события; он обычно реализуется с помощью шины обслуживания или аналогичные артефакт как [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) с помощью [разделы и подписки](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).

Приложения на основе микрослужбу часто будет использовать сочетание этих стилей связи. Наиболее распространенным типом является один получатель связь с синхронной протокол, такой как HTTP или HTTPS при вызове метода регулярное службы Web API HTTP. Микрослужбами также обычно используют протоколы обмена сообщениями для асинхронной связи между микрослужбами.

Полезно знать, чтобы иметь ясности на механизмы возможные связи, но они не являются важные вопросы при построении микрослужбами используются эти оси. Асинхронной природой выполнение потока клиента даже асинхронной природой выбранного протокола являются важных моментов при интеграции микрослужбами. Что *—* важным является возможность интегрировать ваш микрослужбами асинхронно сохранением независимости от микрослужбами, как описано в следующем разделе.

## <a name="asynchronous-microservice-integration-enforces-microservices-autonomy"></a>Асинхронные микрослужбу принудительно автономность микрослужбу элемента

Как уже упоминалось, важно при построении приложения на основе микрослужбами является способом интеграции вашего микрослужбами. В идеальном случае следует попытаться свести к минимуму обмен данными между внутренней микрослужбами. Меньше взаимодействия между микрослужбами, тем лучше. Но Конечно, во многих случаях необходимо интегрировать микрослужбами каким-либо образом. При необходимости для этого правило критического является, обмен данными между микрослужбами должен быть асинхронным. Это не означает наличие использование определенного протокола (например, асинхронный обмен сообщениями и синхронный HTTP). Просто означает, обмен данными между микрослужбами может выполнять только передача данных асинхронно, что старайтесь не зависят от других внутренних микрослужбами как часть операции запроса и ответа HTTP начальной службы.

Если это возможно никогда не зависят от синхронной связи между несколькими микрослужбами, даже для запросов (запрос ответ). Каждый микрослужбу предназначена для того, чтобы быть автономными и доступно для потребителя клиента, даже если другие службы, которые являются частью приложения начала до конца вниз или неработоспособное. Если вы считаете, что необходимо вызвать один микрослужбу других микрослужбами (например, при выполнении запроса HTTP для запроса данных) в, чтобы предоставить ответа в клиентское приложение, у вас есть архитектуру, которая не будет устойчивой, если некоторые микрослужбами ошибкой.

Кроме того не только зависимости HTTP между микрослужбами, как и при создании много циклов запросов и ответов HTTP-запрос цепочки, как показано в первой части 4 Рисунок-15, приводит к микрослужбами не автономной, но также является их производительности так как только одна из служб в этой цепочке низкую производительность. 

Чем больше добавляется синхронной зависимости между микрослужбами, такие как запросы, хуже возвращает общее время ответа для клиентских приложений.

![](./media/image15.png)

**Рис. 4-15**. Антишаблоны и шаблонов в связи между микрослужбами

Если ваш микрослужбу должен вызывать дополнительные действия в другой микрослужбу, если это возможно, не выполнить это действие синхронно и как часть исходной операции запросов и ответов микрослужбы. Это можно сделать асинхронно (с помощью асинхронного обмена сообщениями или события интеграции, очереди, и т. д.). Однако, по возможности, не вызвать действие синхронно в рамках исходного синхронной операции запроса и ответа.

И, наконец, и это, где большинство вопросов, возникающих при построении микрослужбами, если ваш исходный микрослужбу должны изначально, владельцем которого является другой микрослужбами, не следует полагаться на внесение синхронных запросов к этим данным. Вместо этого реплицировать или распространить эти данные (только необходимые атрибуты, которые) в службе начальной базы данных с помощью окончательной согласованности (обычно с помощью события интеграции, как описано в следующих разделах).

Как уже упоминалось в разделе [определение границ модель домена для каждого микрослужбу](#identifying-domain-model-boundaries-for-each-microservice), дублирование некоторые данные через несколько микрослужбами не неверный подход — с другой стороны, при выполнении, который может транслировать данные в определенном языке и условия этого дополнительного домена или ограниченного контекста. Например, в [eShopOnContainers](http://aka.ms/MicroservicesArchitecture) приложения имеют микрослужбу, с именем identity.api, ответственный за большую часть данных пользователя с сущность с именем пользователя. Тем не менее при необходимости хранить данные о пользователе в микрослужбу упорядочения элементов можно сохранить ее в качестве другую сущность с именем покупателей. Покупатель сущности имеет то же удостоверение с исходной сущности пользователя, но он может быть несколько атрибутов, необходимые для упорядочения элементов домена, а не весь профиль.

Можно использовать любой протокол обмена данными и распространения данных асинхронно через микрослужбами для окончательной согласованности. Как уже упоминалось, можно использовать события интеграции с помощью событий шины или сообщений посредника или даже использовать HTTP опрашивая других служб. Он не имеет значения. Главное правило — не создают синхронные зависимости между вашей микрослужбами.

Ниже описаны различные стили связи, рассмотрите возможность использования в приложении микрослужбы.

## <a name="communication-styles"></a>Стили связи

Существует множество протоколов и варианты, которые можно использовать для взаимодействия, в зависимости от типа связи, которые вы хотите использовать. При использовании механизма синхронной связи на основе запроса/ответа протоколов, таких как HTTP, так и REST подход наиболее распространены, особенно при развертывании служб за пределами кластера узла или микрослужбу Docker. Если необходимо обмениваться данными между службами (внутри кластера узла или микрослужбами Docker) можно также использовать механизмы взаимодействия двоичный формат (например, удаленное взаимодействие Service Fabric или WCF с помощью TCP и в двоичном формате). Кроме того можно использовать механизмы асинхронной связи на основе сообщения, такие как AMQP.

Также существует несколько форматов сообщений, как JSON или XML или даже двоичных форматов, которые могут быть более эффективными. Если ваш выбранного двоичного формата не является стандартом, скорее всего, не рекомендуется, публично Публикация служб в этом формате. Можно использовать нестандартный формат для внутренней связи между вашей микрослужбами. Это делается при обмене данными между микрослужбами в Docker узла или микрослужбу кластера (Docker orchestrators или Azure Service Fabric) или для собственных клиентских приложений, которые обращаются к микрослужбами.

### <a name="requestresponse-communication-with-http-and-rest"></a>Запрос ответ связь с HTTP и REST 

Если клиент использует взаимодействия запрос ответ, он отправляет запрос к службе, а затем процессы службы запрос и отправляет ответ обратно. Взаимодействия запрос ответ особенно хорошо подходит для запроса данных в режиме реального времени пользовательского интерфейса (динамической пользовательский интерфейс) из клиентских приложений. Таким образом в архитектуре микрослужбу, скорее всего, используется этот механизм обмена данными для большинства запросов, как показано на рисунке 4-16.

![](./media/image16.png)

**На рисунке 4 – 16**. С помощью запросов и ответов взаимодействие по протоколу HTTP (синхронный или асинхронный)

Клиент использует взаимодействия запрос ответ, предполагается, что ответ будут доставлены за короткий промежуток времени, обычно менее секунды или через несколько секунд не более. Для отложенной ответов необходимо реализовать асинхронную связь на основе [обмена сообщениями](https://docs.microsoft.com/azure/architecture/patterns/category/messaging) и [технологий обмена сообщениями](https://en.wikipedia.org/wiki/Message-oriented_middleware), который является другой подход, который рассматривается в следующем разделе.

Популярный архитектурный стиль для взаимодействия запросов и ответов — [REST](https://en.wikipedia.org/wiki/Representational_state_transfer). Этот подход основан, а также тесно связана с, [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) протокола, в рамках команды HTTP, такие как GET, POST и ПОМЕСТИТЬ. REST подход наиболее часто используемые архитектуры связи при создании службы. Службы REST можно реализовать при разработке веб-API ASP.NET Core services.

При использовании служб HTTP REST в качестве языка определения интерфейса нет никакой ценности. Например при использовании [метаданных Swagger](http://swagger.io/) для описания API-Интерфейс службы, можно использовать средства, создав заглушки клиента, можно напрямую обнаружение и использование служб.

### <a name="additional-resources"></a>Дополнительные ресурсы

-   **Мартин Фоулер (Martin Fowler). Модель зрелости Ричардсон.** Описание модели REST.
    [*http://martinfowler.com/articles/richardsonMaturityModel.HTML*](http://martinfowler.com/articles/richardsonMaturityModel.html)

-   **Swagger.** Официальный сайт.
    [*http://swagger.IO/*](http://swagger.io/)

### <a name="push-and-real-time-communication-based-on-http"></a>Push-уведомлений и в режиме реального времени соединения по протоколу HTTP

Другой вариант (обычно для разных целей, чем REST) — в режиме реального времени и один ко многим обмен данными с платформами более высокого уровня, таких как [ASP.NET SignalR](https://www.asp.net/signalr) и протоколов, таких как [WebSockets](https://en.wikipedia.org/wiki/WebSocket).

Как показано на рисунке 4-17, в режиме реального времени соединения по протоколу HTTP означает, что можно иметь серверный код помещает содержимое подключенных клиентов, когда данные становятся доступны, а не ждать клиента для запроса новых данных сервера.

![](./media/image17.png)

**На рисунке 4-17**. Один к одному в режиме реального времени асинхронный обмен сообщениями

Поскольку связи находится в режиме реального времени, клиентские приложения практически мгновенно отображать изменения. Это обычно обрабатываются протокол, например WebSockets, с помощью большого количества подключений WebSockets (по одному для каждого клиента). Типичным примером является служба, взаимодействующие изменение оценка игры спортивных множество клиентских веб-приложениям одновременно.


>[!div class="step-by-step"]
[Предыдущие] (direct-client-to-microservice-communication-versus-the-api-gateway-pattern.md) [Далее] (асинхронной сообщения — на основе communication.md)