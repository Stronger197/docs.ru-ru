---
title: Практическое руководство. Поиск потомков с определенным именем элемента (C#)
ms.date: 07/20/2015
ms.assetid: f684da20-bee9-47f5-9607-7e3fd7e67470
ms.openlocfilehash: 6c5e035b4ee0168a0c41a34754314e18d089b1ef
ms.sourcegitcommit: 3c1c3ba79895335ff3737934e39372555ca7d6d0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/06/2018
ms.locfileid: "43861423"
---
# <a name="how-to-find-descendants-with-a-specific-element-name-c"></a>Практическое руководство. Поиск потомков с определенным именем элемента (C#)
Иногда возникает необходимость найти всех потомков с определенным именем. В таких случаях можно написать код для просмотра всех потомков, но проще использовать ось <xref:System.Xml.Linq.XContainer.Descendants%2A>.  
  
## <a name="example"></a>Пример  
 В следующем примере показано, как находить потомков на основе имени элемента.  
  
```csharp  
XElement root = XElement.Parse(@"<root>  
  <para>  
    <r>  
      <t>Some text </t>  
    </r>  
    <n>  
      <r>  
        <t>that is broken up into </t>  
      </r>  
    </n>  
    <n>  
      <r>  
        <t>multiple segments.</t>  
      </r>  
    </n>  
  </para>  
</root>");  
IEnumerable<string> textSegs =  
    from seg in root.Descendants("t")  
    select (string)seg;  
  
string str = textSegs.Aggregate(new StringBuilder(),  
    (sb, i) => sb.Append(i),  
    sp => sp.ToString()  
);  
  
Console.WriteLine(str);  
```  
  
 Этот код выводит следующие результаты:  
  
```  
Some text that is broken up into multiple segments.  
```  
  
## <a name="example"></a>Пример  
 Следующий пример демонстрирует тот же запрос XML, что и в пространстве имен. Дополнительные сведения см. в разделе [Работа с пространствами имен XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```csharp  
XElement root = XElement.Parse(@"<root xmlns='http://www.adatum.com'>  
  <para>  
    <r>  
      <t>Some text </t>  
    </r>  
    <n>  
      <r>  
        <t>that is broken up into </t>  
      </r>  
    </n>  
    <n>  
      <r>  
        <t>multiple segments.</t>  
      </r>  
    </n>  
  </para>  
</root>");  
XNamespace ad = "http://www.adatum.com";  
IEnumerable<string> textSegs =  
    from seg in root.Descendants(ad + "t")  
    select (string)seg;  
  
string str = textSegs.Aggregate(new StringBuilder(),  
    (sb, i) => sb.Append(i),  
    sp => sp.ToString()  
);  
  
Console.WriteLine(str);  
```  
  
 Этот код выводит следующие результаты:  
  
```  
Some text that is broken up into multiple segments.  
```  
  
## <a name="see-also"></a>См. также

- <xref:System.Xml.Linq.XContainer.Descendants%2A>  
- [Базовые запросы (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/basic-queries-linq-to-xml.md)
