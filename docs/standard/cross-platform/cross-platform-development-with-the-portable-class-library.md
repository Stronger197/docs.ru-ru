---
title: Кроссплатформенная разработка с переносной библиотекой классов
ms.date: 09/17/2018
ms.technology: dotnet-standard
helpviewer_keywords:
- Portable Class Library [.NET Framework]
- targeting multiple platforms
- multiple platforms, targeting
ms.assetid: c31e1663-c164-4e65-b66d-d3aa8750a154
author: mairaw
ms.author: mairaw
ms.openlocfilehash: afaa8e118bb21e5c1e4f1c53b1d0d29ca6bb3bf5
ms.sourcegitcommit: ea00c05e0995dae928d48ead99ddab6296097b4c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/02/2018
ms.locfileid: "48030844"
---
# <a name="cross-platform-development-with-the-portable-class-library"></a>Кроссплатформенная разработка с переносимой библиотекой классов

Тип проекта переносимой библиотеки классов в Visual Studio поможет вам быстро и легко создавать кросс платформенные приложения и библиотеки для платформ Майкрософт.

[!INCLUDE[standard](../../../includes/pcl-to-standard.md)]

Переносимые библиотеки классов уменьшают временные и трудовые затраты на разработку и тестирования кода. Используйте этот тип проекта для написания кода и сборки переносимых сборок .NET Framework, а затем ссылайтесь на них из приложений, предназначенных для нескольких платформ, таких как .NET Framework, iOS или Mac.

Даже после создания проекта переносимой библиотеки классов в Visual Studio и начала работы над проектом вы сможете изменить целевые платформы. Visual Studio компилирует библиотеку с новыми сборками, позволяющий определить изменения, которые необходимо внести в код.

## <a name="create-a-portable-class-library-project"></a>Создание проекта переносимой библиотеки классов

Чтобы создать переносимую библиотеку классов, используйте шаблоном в Visual Studio. Создайте новый проект (**файл** > **новый проект**) и в **новый проект** диалоговом окне выберите язык программирования (Visual C# или Visual Basic). Выберите **библиотека классов (для прежних версий Portable)** шаблона. Введите имя проекта и выберите **ОК**.

**Добавление переносимой библиотеки классов** откроется диалоговое окно. Выберите два или несколько целевых объектов, а затем нажмите **ОК**.

![Добавить целевые объекты библиотеке переносных классов в Visual Studio](media/add-portable-class-library.png)

## <a name="change-targets"></a>Изменить цели

Можно изменить целевые платформы из проекта переносимой библиотеки классов, при ее создании или после начала разработки. Если вы хотите изменить целевые платформы после создания проекта, в **обозревателе решений**, откройте контекстное меню для проекта переносимой библиотеки классов (не решение) и затем выберите **свойства** . На странице свойств проекта **библиотеки** вкладке отображается платформ, в данный момент нацелен проект.

![Свойства проекта для переносимой библиотеки классов в Visual Studio](media/pcl-project-properties.png)

Чтобы добавить или удалить целевые объекты, выберите **изменение** кнопку и затем установите или снимите соответствующие флажки.

При изменении целевых платформ API-интерфейсы, доступные для разработки проекта, изменятся в соответствии с выбранными платформами. Visual Studio отображает ошибки и предупреждения после изменения целевых платформ.

Если вы хотите оценить переносимость сборки до можно внести изменения в Visual Studio, можно использовать [анализатор переносимости .NET](https://visualstudiogallery.msdn.microsoft.com/1177943e-cfb7-4822-a8a6-e56c7905292b).

## <a name="supported-types-and-members"></a>Поддерживаемые типы и члены

Типы и члены, доступные в проектах переносимой библиотеки классов, ограничены несколькими факторами совместимости:

-   они должны быть общими для выбранных целевых платформ;

-   они должны вести себя аналогичным образом на всех этих платформах;

-   они не должны быть кандидатами на вывод из употребления;

-   они должны иметь смысл в переносимой среде, особенно если вспомогательные члены не являются переносимыми.

Если член поддерживается в переносимой библиотеке классов и для выбранных целевых платформ, он будет показан в IntelliSense в вашем проекте. Однако помните, что интерфейс API может поддерживаться в переносимой библиотеки классов, но возможность его использования зависит от выбранных целевых платформ.

## <a name="api-differences-in-the-portable-class-library"></a>Отличия API в переносимой библиотеке классов

Для обеспечения совместимости сборок переносимой библиотеки классов на всех поддерживаемых платформах некоторые члены в переносимой библиотеке классов были немного изменены.

## <a name="use-the-portable-class-library"></a>Использование переносимой библиотеки классов

После построения проекта переносимой библиотеки классов просто добавьте ссылку на нее в других проектах. Можно сделать ссылку на проект или на конкретные сборки, содержащие классы, к которым требуется доступ.

Для запуска приложения, ссылающегося на сборку переносимой библиотеки классов, на компьютере должны быть установлены требуемые (или более поздние) версии целевых платформ. Visual Studio содержит все необходимые платформы, поэтому приложение можно запустить без дальнейших изменений на компьютере, который использовался для его разработки.

### <a name="deploy-a-universal-windows-app"></a>Развернуть приложение универсальной Windows

При создании приложения универсальной Windows, ссылающийся на сборку переносимой библиотеки классов, все необходимые для развертывания приложения уже включено в пакет приложения и никаких дальнейших действий не требуется.

### <a name="deploy-a-net-framework-app"></a>Развертывание .NET Framework приложения

При развертывании приложения .NET Framework, в котором имеется ссылка на сборку переносимой библиотеки классов, необходимо задать зависимость от нужной версии платформы .NET Framework. Задание этой зависимости обеспечивает установку нужной версии вместе с приложением.

-   Чтобы создать зависимость с развертыванием ClickOnce: В **обозревателе решений**, выберите узел проекта для проекта, необходимо опубликовать. (Это проект, в котором имеется ссылка на проект переносимой библиотеки классов.) В строке меню выберите **проекта** > **свойства**и нажмите кнопку **публикации** вкладки. На **публикации** выберите **предварительные требования**. Отметьте требуемую версию платформы .NET Framework как необходимый компонент.

-   Чтобы создать зависимость с проектом установки: В **обозревателе решений**, выберите проект установки. В строке меню выберите **проекта** > **свойства** > **предварительные требования**. Отметьте требуемую версию платформы .NET Framework как необходимый компонент.

Дополнительные сведения о развертывании приложений .NET Framework, см. в разделе [руководство по развертыванию для разработчиков](../../../docs/framework/deployment/deployment-guide-for-developers.md).

## <a name="see-also"></a>См. также

- [Использование переносимой библиотеки классов с MVVM](../../../docs/standard/cross-platform/using-portable-class-library-with-model-view-view-model.md)
- [Ресурсы приложений для библиотек, предназначенных для нескольких платформ](../../../docs/standard/cross-platform/app-resources-for-libraries-that-target-multiple-platforms.md)
- [Анализатор переносимости .NET](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer)
- [Поддержка платформы .NET Framework для приложений магазина Windows и среды выполнения Windows](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)
- [Развертывание](../../../docs/framework/deployment/net-framework-applications.md)
