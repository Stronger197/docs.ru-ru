---
title: Практическое руководство. Явная реализация членов двух интерфейсов (Руководство по программированию на C#)
ms.date: 07/20/2015
helpviewer_keywords:
- inheritance [C#], explicitly implementing interface members
- interfaces [C#], explicitly implementing with inheritance
ms.assetid: 8b402ddc-dff9-4869-89cb-d718c764e68e
ms.openlocfilehash: 6c02585b57acef654c6613bef1a276a433763af6
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43514677"
---
# <a name="how-to-explicitly-implement-members-of-two-interfaces-c-programming-guide"></a>Практическое руководство. Явная реализация членов двух интерфейсов (Руководство по программированию на C#)
Явная реализация [интерфейсов](../../../csharp/language-reference/keywords/interface.md) позволяет разработчику реализовать два интерфейса с одинаковыми именами членов и создать отдельные реализации каждого члена интерфейса. В этом примере размеры поля выводятся в метрической и английской системе мер. [Класс](../../../csharp/language-reference/keywords/class.md) Box реализует два интерфейса (IEnglishDimensions и IMetricDimensions), представляющие соответствующие системы мер. В обоих интерфейсах представлены члены с одинаковыми именами: Length и Width.  
  
## <a name="example"></a>Пример  
 [!code-csharp[csProgGuideInheritance#9](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-explicitly-implement-members-of-two-interfaces_1.cs)]  
  
## <a name="robust-programming"></a>Отказоустойчивость  
 Если требуется использовать единицы английской системы мер по умолчанию, реализуйте методы Length и Width обычным способом, после чего явно реализуйте методы Length и Width из интерфейса IMetricDimensions:  
  
 [!code-csharp[csProgGuideInheritance#10](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-explicitly-implement-members-of-two-interfaces_2.cs)]  
  
 В этом случае единицы английской системы мер будут доступны из экземпляра класса, а метрические единицы — из экземпляра интерфейса:  
  
 [!code-csharp[csProgGuideInheritance#11](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-explicitly-implement-members-of-two-interfaces_3.cs)]  
  
## <a name="see-also"></a>См. также

- [Руководство по программированию на C#](../../../csharp/programming-guide/index.md)  
- [Классы и структуры](../../../csharp/programming-guide/classes-and-structs/index.md)  
- [Интерфейсы](../../../csharp/programming-guide/interfaces/index.md)  
- [Практическое руководство. Явная реализация членов интерфейса](../../../csharp/programming-guide/interfaces/how-to-explicitly-implement-interface-members.md)
