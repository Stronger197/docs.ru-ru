---
title: Создание XML-документа
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
ms.assetid: 877e9c62-b082-4bfb-bc5b-f47297eb30ef
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b76140fb7d79b1e191c0451cd7556963130d224a
ms.sourcegitcommit: 6eac9a01ff5d70c6d18460324c016a3612c5e268
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/16/2018
ms.locfileid: "45646185"
---
# <a name="xml-document-creation"></a>Создание XML-документа
XML-документ можно создать двумя способами. Один из них заключается в создании объекта **XmlDocument** без параметров. Второй включает создание объекта **XmlDocument**, которому нужно в качестве параметра передать XmlNameTable. В следующем примере показано создание пустого объекта **XmlDocument** без параметров.  
  
```vb  
Dim doc As New XmlDocument()  
```  
  
```csharp  
XmlDocument doc = new XmlDocument();  
```  
  
 После создания документа в него можно с помощью метода **Load** загрузить данные из строки, потока, URL-адреса, текстового модуля чтения или класса, производного от **XmlReader**. Есть еще один метод загрузки: **LoadXML**, который считывает XML из строки. Дополнительные сведения о различных методах **Load** см. в статье [Считывание XML-документа в DOM](../../../../docs/standard/data/xml/reading-an-xml-document-into-the-dom.md).  
  
 Существует класс с именем **XmlNameTable**. Он является таблицей атомарных объектов строки. Эта таблица предоставляет средству синтаксического анализа XML эффективный способ использовать один и тот же строковый объект для всех повторяющихся имен элементов и атрибутов в XML-документе. Класс **XmlNameTable** автоматически создается при создании документа, как показано выше, и заполняется именами элементов и атрибутов при загрузке этого документа. Если у вас уже есть документ с таблицей имен и эти имена можно применить в другом документе, создайте новый документ с помощью метода **Load**, передав ему в качестве параметра таблицу **XmlNameTable**. Когда документ создается с помощью этого метода, он использует существующую таблицу **XmlNameTable** со всеми атрибутами и элементами, ранее загруженными в нее из другого документа. Это можно использовать для эффективного сравнения имен элементов и атрибутов. Дополнительные сведения о классе **XmlNameTable** см. в таблице [Сравнение объектов с помощью XmlNameTable](../../../../docs/standard/data/xml/object-comparison-using-xmlnametable.md). Справочную информацию см. в статье <xref:System.Xml.XmlNameTable>.  
  
## <a name="see-also"></a>См. также

- [Модель объектов документов XML (DOM)](../../../../docs/standard/data/xml/xml-document-object-model-dom.md)
