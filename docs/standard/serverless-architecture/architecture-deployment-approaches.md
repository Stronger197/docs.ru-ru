---
title: Подходы к архитектуре развертывания - Бессерверных приложений
description: Руководство по разному корпоративных архитектур, развернутых в облаке, с помощью сравнение IaaS, PaaS, контейнеры и без сервера.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 6566971d8984ec046b8b5fa2db295c1d48c30b20
ms.sourcegitcommit: 4c158beee818c408d45a9609bfc06f209a523e22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/03/2018
ms.locfileid: "49370213"
---
# <a name="architecture-deployment-approaches"></a>Подходы к архитектуре развертывания

Независимо от архитектуры подход, используемый при создании бизнес-приложения, реализация или развертывание этих приложений могут различаться. Предприятиям ведущим приложениям все — от физического оборудования бессерверные функции.

## <a name="n-tier-applications"></a>N-уровневых приложениях

[Шаблон архитектуры N-уровневых](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier) зрелой архитектуры и просто относится к приложениям, которые разделяют различные логические слои в отдельные физические уровни. N-уровневая архитектура является физической реализации архитектуры N-Слойных. Наиболее распространенная реализация такой архитектуры включает в себя:

* Уровень представления, например веб-приложения.
* API или данных уровня доступа, например интерфейсу API REST.
* Уровень данных, таких как базы данных SQL.

![N-уровневой архитектуре](./media/n-tier-architecture.png)

N-уровневого решения имеют следующие характеристики:

* Проекты обычно согласованы с уровнями.
* Тестирование может быть близки по-разному по уровням.
* Уровни позволяют уровни абстракции, например на уровне представления обычно относительно этих подробностей реализации уровня данных.
* Как правило только взаимодействия слоев с соседних слоев.
* Выпуски часто осуществляется в проект и поэтому уровень, уровень. Простое изменение API может потребоваться новый выпуск всей среднего уровня.

Такой подход обеспечивает несколько преимуществ, включая:

* Изоляция базы данных (часто переднего плана не имеет прямой доступ к серверной части базы данных).
* Повторно использовать API-интерфейса (для примера, мобильные, Классические приложения и веб-приложений клиентов можно использовать те же интерфейсы API).
* Возможность масштабирования уровни независимо друг от друга.
* Рефакторинг изоляции: одного уровня может быть выполнен рефакторинг без влияния на другие уровни.

## <a name="on-premises-and-infrastructure-as-a-service-iaas"></a>В локальных и инфраструктура как услуга (IaaS)

Традиционный подход к размещению приложений требуется приобретение оборудования и управления ими, все установки программного обеспечения, включая операционную систему. Изначально это участвует центрах обработки данных и физическим оборудованием. Сложности, связанные с физическим оборудованием операционной их множество, включая:

* Необходимость приобрести лишние для «всякий случай» или пиковой нагрузки сценариев спроса.
* Защита физического доступа к оборудованию.
* Ответственность за аппаратного сбоя (например, ошибка диска).
* Охлаждение.
* Настройка, маршрутизаторы и подсистемы балансировки нагрузки.
* Резервирования питания.
* Обеспечение безопасности доступ к программному обеспечению.

![Модель IaaS](./media/iaas-approach.png)

Виртуализация оборудования, с помощью «виртуальные машины» позволяет инфраструктуры как услуги (IaaS). Хост-компьютерах эффективно бывают секционированы для предоставления ресурсов для экземпляров с выделением для своих собственных память, ЦП и хранилища. Команда подготавливает необходимые виртуальные машины и настраивает связанных сетей и доступ к хранилищу.

Дополнительные сведения см. в разделе [виртуальной машины эталонной архитектуры N-уровневого](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier).

Несмотря на то, что виртуализация и инфраструктура как услуга (IaaS) устранения многих проблем, по-прежнему оставляет широкими полномочиями в руки группы инфраструктуры. Команда поддерживает версии операционной системы, применяет исправления системы безопасности и устанавливает зависимости сторонних на целевых компьютерах. Приложения зачастую ведут себя иначе на рабочих компьютерах по сравнению с тестовой среды. Проблемы возникают из-за зависимостей для различных версий и/или SKU операционной системы уровней. Несмотря на то, что во многих организациях развертывание N-уровневые приложения для этих целевых объектов, многие компании преимущества от развертывания в модель дополнительные собственного облака, такие как [платформа как услуга](#platform-as-a-service-paas). Архитектур с микрослужбами являются более сложной задачей из-за требований к горизонтальное масштабирование для эластичности и устойчивости.

Дополнительные сведения см. в разделе [виртуальные машины](https://docs.microsoft.com/azure/virtual-machines/).

## <a name="platform-as-a-service-paas"></a>Платформа как услуга (PaaS)

Платформа как услуга (PaaS) предлагает настроить решения, которые разработчики могут подключить в непосредственно. PaaS — другое название для управляемого размещения. Это устраняет необходимость управления базовой операционной системы, безопасности, исправления, а во многих случаях зависимые компоненты независимых производителей. Примеры платформ веб-приложений, баз данных, и серверной части мобильных.

PaaS трудности, общие для IaaS. PaaS позволяет разработчику сосредоточиться на код или схемы базы данных, а не как развертывается. Преимущества PaaS:

* Платите за использование моделей, исключить дополнительные затраты вкладывает средства в простоя машин.
* Направьте развертывания и улучшенная DevOps, Непрерывная интеграция (CI) и конвейеры непрерывной поставки (CD).
* Автоматические обновления, обновлений и исправлений безопасности.
* Сигнал увеличения или уменьшения вверх (гибкое масштабирование).

Главным недостатком PaaS традиционно была поставщику. Например некоторые поставщики услуг PaaS поддерживают только ASP.NET, Node.js, или других определенных языков и платформ. Продукты, такие как службы приложений Azure используют адрес нескольких платформ и поддерживающих широкий спектр языков и платформ для размещения веб-приложений.

![Платформа как архитектура службы](./media/paas-architecture.png)

## <a name="software-as-a-service-saas"></a>Программное обеспечение как услуга (SaaS)

Программное обеспечение как служба или SaaS централизованно размещенные и доступны без локальной установки или подготовки. SaaS часто размещается поверх PaaS как платформа для развертывания программного обеспечения. SaaS предоставляет службы для запуска и подключения с существующим программным обеспечением. SaaS — часто отрасли и конкретных по вертикали. SaaS лицензируется часто и обычно предоставляет модель клиент сервер. Большинство современных предложения SaaS использовать веб-приложения для клиента. Компании обычно можно считать SaaS бизнес-решение для предложения лицензий. Он часто не реализуется в виде рассмотрения архитектуры для обеспечения масштабируемости и сопровождения больших приложений. В самом деле большинство решений SaaS основаны на IaaS, PaaS или бессерверные серверных частей.

Подробнее о SaaS через [пример приложения](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app).

## <a name="containers-and-functions-as-a-service-faas"></a>Контейнеры и функции как услугу (FaaS)

Контейнеры — это интересное решение, которое включает преимущества PaaS по принципу без издержек на IaaS. Контейнер — по существу среду выполнения, которая содержит самые необходимые, необходимые для выполнения уникальные приложения. Компонент ядра или ядра операционной системы и служб, таких как хранилище являются общими для узла. Общее ядро позволяет контейнерам упрощенные (некоторые являются простым МБ, по сравнению с размером гигабайт типичный виртуальных машин). На узлах, уже под управлением контейнеры можно быть быстро приступить к работе, обеспечению высокого уровня доступности. Возможность быстро запускайте контейнеры также предоставляет дополнительные уровни устойчивости. Docker является одним из наиболее популярных реализаций контейнеров.

Преимущества контейнеров:

* Упрощенная и переносимый
* Автономное таким образом, нет необходимости устанавливать зависимости
* Обеспечивают согласованную среду независимо от того узла, (запускается на переносном компьютере так же, как на сервере облака)
* Можно быстро подготовить для горизонтального масштабирования
* Можно быстро перезапустить для восстановления после сбоя

Контейнер выполняется на узле контейнера (который в свою очередь может запускаться на физической машины или виртуальной машины). Несколько контейнеров или экземпляров из тех же контейнеров могут выполняться на одном узле. Значение true, отработки отказа и устойчивости контейнеры должны масштабироваться на узлах.

Дополнительные сведения о контейнерах см. в разделе [что такое Docker](../microservices-architecture/container-docker-introduction/docker-defined.md)?

Управление контейнерами на узлах обычно требуется средство оркестрации, например Kubernetes. Настройка и управление решениями оркестрации могут добавлять в проекты дополнительных издержек и сложности. К счастью многие поставщики облачных услуг предоставляют службы оркестрации с помощью решений PaaS, чтобы упростить управление контейнеров.

На следующем рисунке показан пример установки Kubernetes. Узлы установки адрес масштабирования и отработки отказа. Они выполняются Docker экземпляры контейнеров, которые управляются главного сервера. *Kubelet* — клиент, который передает команды Docker с помощью Kubernetes.

![Kubernetes](./media/kubernetes-example.png)

Дополнительные сведения об оркестрации, см. в разделе [Kubernetes в Azure](https://docs.microsoft.com/azure/aks/intro-kubernetes).

Функции как услугу (FaaS) — это специализированный контейнера служба, которая аналогична без сервера. Определенная реализация FaaS, вызывается [OpenFaaS](https://github.com/openfaas/faas), располагается поверх контейнеров для предоставления возможностей без сервера. OpenFaaS содержит шаблоны, упаковать все зависимости контейнера, необходимо выполнить фрагмент кода. С помощью шаблонов упрощает процесс развертывания кода как единую функциональную единицу. OpenFaaS предназначен для архитектуры, уже содержащим контейнеров и оркестраторы, так как он может использовать существующую инфраструктуру. Несмотря на то, что он предоставляет бессерверные функции, он специально требует использовать Docker и оркестратора.

## <a name="serverless"></a>Без сервера

Бессерверная архитектура обеспечивает четкое разделение между кодом и средой размещения. Вы реализуете код в *функция* , активируемые *триггера*. После завершения работы этой функции можно освободить все необходимые ресурсы. Триггер может быть вручную, истекло время ожидания процесса, HTTP-запроса или передачи файлов. Триггер образом выполнение кода. Хотя зависит от бессерверные платформы, наиболее предоставляют доступ к предварительно определенных API-интерфейсы и привязки для упрощения выполнения задач, например, запись базы данных или очередь результаты.

Бессерверной архитектуры, во многом полагается на абстрагирования хост-среды, чтобы сосредоточиться на коде. Он может рассматриваться как *меньше server*.

Контейнер решения предоставляют существующие разработчикам создавать скрипты для публикации кода без сервера готовых образов. В других реализациях использовать существующие решения PaaS для предоставления масштабируемой архитектуры.

Абстракция означает, что команда DevOps не нужно подготавливать или администрировать серверы, а также конкретных контейнеров. Код бессерверной платформе узлов, либо как сценарии или исполняемые файлы упакованные связанных пакета SDK для и выделяет ресурсы, необходимые для кода для масштабирования.

На рисунке диаграммы четырех бессерверных компонентов. Запрос HTTP вызывает код извлечения API для выполнения. API извлечения вставляет код в базу данных, и некоторые другие функции для выполнения задачи, такие как вычислительные задачи и выполнении порядок триггеров insert.

![Реализация без сервера](./media/serverless-implementation.png)

Преимущества бессерверных:

* **Высокая плотность.** На одном узле, по сравнению с контейнеров или виртуальных машин можно запустить несколько экземпляров того же кода без сервера. Масштаб экземпляры в нескольких узлах масштабирования и устойчивости.
* **Выставление счетов Micro**. В зависимости от выполнения без сервера, экономии большие в определенных сценариях наиболее бессерверной спецификации поставщиков.
* **Быстрое масштабирование**. Без использования сервера могут масштабироваться в соответствии рабочих нагрузок, быстро и автоматически.
* **Время выхода на рынок** разработчикам сосредоточиться на коде, а также развертывание непосредственно на бессерверной платформе. Компоненты могут быть сняты независимо друг от друга.

Независимая чаще всего рассматривается в контексте вычислений, но также можно применить к данным. Например [Azure SQL](https://docs.microsoft.com/azure/sql-database) и [Cosmos DB](https://docs.microsoft.com/azure/cosmos-db) предоставляют облачным базам данных, которые не требуют настройки хост-компьютеров или кластеров. Эта книга посвящена бессерверных вычислений.

## <a name="summary"></a>Сводка

Существует широкий спектр доступных вариантов для архитектуры, включая гибридный подход. Независимая упрощает подход, управления и затрат возможностей приложений за счет управления и переносимость. Тем не менее многие бессерверной платформы предоставляют конфигурацию для дополнительной настройки решения. Рекомендуемые методы программирования также может привести к более переносимый код и менее блокировки в бессерверной платформе. В следующей таблице показано подходы к архитектуре рядом друг с другом. Выберите без сервера на основе масштабируемого потребностей ли вы хотите управлять среда выполнения и насколько хорошо ваши рабочие нагрузки можно разбить на небольших компонентов. Вы узнаете о потенциальных проблем благодаря бессерверной архитектуре и другие точки принятия решений в следующей главе.

|         |IaaS     |PaaS     |Контейнер|Без сервера|
|---------|---------|---------|---------|----------|
|**Масштаб**|ВИРТУАЛЬНОЙ МАШИНЫ       |Экземпляр |Приложение      |Функция  |
|**Краткие описания**|Оборудование|Platform|ОС узла|Среда выполнения   |
|**Единица** |ВИРТУАЛЬНОЙ МАШИНЫ       |Проект  |Изображение    |Код      |
|**Время существования**|месяцев|Дней до месяцев|Минут до дней|Время в миллисекундах минут|
|**ответственность за**|Приложения, зависимости, среда выполнения и операционной системы|Приложения и зависимости|Приложения, зависимости и среды выполнения|Функция

* **Масштаб** ссылается единицей, которая используется для масштабирования приложения
* **Абстрагирует** ссылается на слой, на котором извлекается с помощью реализации
* **Единица** относится к тому, что развернуто область
* **Время существования** ссылается на типичные среды выполнения конкретного экземпляра
* **Ответственность за** ссылается на издержки, чтобы создавать, развертывать и обслуживать приложения

Следующей главе будут сосредоточиться на бессерверной архитектуры, варианты использования и шаблоны разработки.

## <a name="recommended-resources"></a>Рекомендуемые ресурсы

* [Руководство по архитектуре приложений Azure](https://docs.microsoft.com/azure/architecture/guide/)
* [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db)
* [Azure SQL](https://docs.microsoft.com/azure/sql-database)
* [Шаблон N-уровневой архитектуре](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/n-tier)
* [Kubernetes в Azure](https://docs.microsoft.com/azure/aks/intro-kubernetes)
* [Микрослужбы](https://docs.microsoft.com/azure/architecture/guide/architecture-styles/microservices)
* [Эталонной архитектуры N-уровневого виртуальной машины](https://docs.microsoft.com/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)
* [Виртуальные машины](https://docs.microsoft.com/azure/virtual-machines/)
* [Что такое Docker?](../microservices-architecture/container-docker-introduction/docker-defined.md)
* [Приложение Wingtip Tickets SaaS](https://docs.microsoft.com/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)

>[!div class="step-by-step"]
[Назад](architecture-approaches.md)
[Вперед](serverless-architecture.md)