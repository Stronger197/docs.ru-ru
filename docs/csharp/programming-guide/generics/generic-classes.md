---
title: Универсальные классы (Руководство по программированию на C#)
ms.date: 07/20/2015
helpviewer_keywords:
- C# language, generic classes
- generics [C#], classes
ms.assetid: 27d6f256-cd61-41e3-bc6e-b990a53b0224
ms.openlocfilehash: 2568600c130847b3317aeb399541c61a050901ce
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2018
ms.locfileid: "44216084"
---
# <a name="generic-classes-c-programming-guide"></a>Универсальные классы (Руководство по программированию на C#)
Универсальные классы инкапсулируют операции, которые не относятся к конкретному типу данных. Универсальные классы чаще всего используются для работы с коллекциями, такими как связанные списки, хэш-таблицы, стеки, очереди, деревья и т. д. Такие операции, как добавление и удаление элементов коллекции, по существу выполняются одинаково, независимо от типа хранимых данных.  
  
 В большинстве случаев для этого используются классы коллекций. Рекомендуется выбирать те из них, которые представлены в библиотеке классов платформы .NET. Дополнительные сведения об использовании этих классов см. в разделе [Универсальные коллекции в .NET](../../../standard/generics/collections.md).  
  
 Как правило, при создании универсального класса сначала определяется конкретный класс, после чего его типы поочередно заменяются параметрами типов до тех пор, пока не будет достигнут необходимый баланс между степенью обобщения и удобством работы. При создании собственных универсальных классов необходимо учитывать следующие важные моменты:  
  
-   Типы, которые требуется обобщить с использованием параметров типа.  
  
     Как правило, чем больше типов параметризовано, тем более гибким и универсальным становится ваш код. Тем не менее слишком высокая степень обобщения может отрицательно сказаться на понятности создаваемого вами кода для других разработчиков.  
  
-   Ограничения (если требуются), которые будут применяться к параметрам типа (см. раздел [Ограничения параметров типа](../../../csharp/programming-guide/generics/constraints-on-type-parameters.md)).  
  
     Рекомендуется применять максимально возможный объем ограничений, при котором вы по-прежнему сможете работать с необходимыми типами. Например, если универсальный класс будет использоваться только для работы со ссылочными типами, примените ограничение класса. Это позволит исключить случайное использование класса с типами значений и позволит использовать оператор `as` в отношении `T`, а также проверять наличие значений null.  
  
-   Требуется ли разбивать универсальные функции между базовыми классами и подклассами.  
  
     Поскольку универсальные классы могут выступать в качестве базовых классов, здесь необходимо учитывать те же принципы разработки, что и для классов, не являющихся универсальными. См. описание правил наследования от универсальных базовых классов далее в этом разделе.  
  
-   Требуется ли реализовывать один или несколько универсальных интерфейсов.  
  
     Например, при разработке класса, который будет использоваться для создания элементов коллекции на основе универсальных шаблонов, может потребоваться реализовать интерфейс <xref:System.IComparable%601>, где `T` — это тип вашего класса.  
  
 Пример простого универсального класса можно найти в разделе [Введение в универсальные шаблоны](../../../csharp/programming-guide/generics/introduction-to-generics.md).  
  
 Правила в отношении параметров типа и ограничений влияют на поведение универсального класса, особенно в контексте наследования и доступа к элементам. Прежде чем продолжить, необходимо ознакомиться с некоторыми терминами и понятиями. Ссылка на универсальный класс `Node<T>,` в клиентском коде может задаваться с использованием аргумента типа или путем создания закрытого сконструированного типа (`Node<int>`). Кроме того, можно не задавать параметр типа (например, при указании универсального базового класса), чтобы определить открытый сконструированный тип (`Node<T>`). Универсальные классы могут наследоваться от конкретных, а также закрытых или открытых сконструированных базовых классов:  
  
 [!code-csharp[csProgGuideGenerics#16](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_1.cs)]  
  
 Классы, не являющиеся универсальными, то есть конкретные классы, могут наследоваться от закрытых сконструированных базовых классов. Наследование от аналогичных открытых классов или от параметров типа невозможно, поскольку во время выполнения клиентский код не может предоставить аргумент типа, необходимый для создания экземпляра базового класса.  
  
 [!code-csharp[csProgGuideGenerics#17](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_2.cs)]  
  
 Универсальные классы, наследуемые от открытых сконструированных типов, должны предоставлять аргументы типа для любых параметров типа базового класса, которые не используются совместно с наследующим классом. Это продемонстрировано в следующем коде:  
  
 [!code-csharp[csProgGuideGenerics#18](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_3.cs)]  
  
 Универсальные классы, наследуемые от открытых сконструированных типов, должны задавать множество ограничений, которые явно или косвенно включают в себя все ограничения базового типа:  
  
 [!code-csharp[csProgGuideGenerics#19](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_4.cs)]  
  
 Универсальные типы могут использовать несколько параметров типа и ограничений, как показано ниже:  
  
 [!code-csharp[csProgGuideGenerics#20](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_5.cs)]  
  
 Открытые и закрытые сконструированные типы можно использовать в качестве параметров метода:  
  
 [!code-csharp[csProgGuideGenerics#21](../../../csharp/programming-guide/generics/codesnippet/CSharp/generic-classes_6.cs)]  
  
 Если универсальный класс реализует интерфейс, все экземпляры такого класса можно привести к этому интерфейсу.  
  
 Универсальные классы инвариантны. Другими словами, если входной параметр задает `List<BaseClass>`, при попытке предоставить `List<DerivedClass>` возникает ошибка времени компиляции.  
  
## <a name="see-also"></a>См. также

- <xref:System.Collections.Generic>  
- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Универсальные шаблоны](../../../csharp/programming-guide/generics/index.md)  
- [Сохранение состояния перечислителей](https://blogs.msdn.microsoft.com/wesdyer/2006/01/13/saving-the-state-of-enumerators/)  
- [Загадка по наследованию, часть 1](https://blogs.msdn.microsoft.com/ericlippert/2007/07/27/an-inheritance-puzzle-part-one/)
