---
title: Справочник по API отражения для машинного кода .NET
ms.date: 03/30/2017
ms.assetid: 0429c049-22a3-4ba1-9cc8-f6ee91e31d9c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 13dfdfd89bf91510146ce388620d3e51c2aa1f02
ms.sourcegitcommit: fd8d4587cc26e53f0e27e230d6e27d828ef4306b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/16/2018
ms.locfileid: "49347533"
---
# <a name="net-native-reflection-api-reference"></a>Справочник по API отражения для машинного кода .NET
[!INCLUDE[net_native](../../../includes/net-native-md.md)] включает три новых типа исключений: [System.Runtime.CompilerServices.MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md), [System.Reflection.MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md)и [System.Reflection.MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md). Все эти типы исключений имеют указанные ниже особенности:  
  
 Эти типы предназначены только для внутреннего использования.  
 Эти три типа исключений предназначены только для использования цепочкой инструментов [!INCLUDE[net_native](../../../includes/net-native-md.md)] . Исключения создаются, когда цепочка инструментов [!INCLUDE[net_native](../../../includes/net-native-md.md)] обнаруживает отсутствие данных, из-за которого дальнейшее выполнение программы невозможно.  
  
 Не обрабатывайте эти исключения в своем коде.  
 Эти исключения указывают на отсутствие метаданных (исключения [MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md) и [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) ) или кода реализации (исключение [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) ), которые необходимы вашему приложению. Чтобы устранить причины этих исключений, измените файл директив среды выполнения (RD.XML) так, чтобы необходимые метаданные или код реализации были доступны во время выполнения. Дополнительные сведения см. в разделе [Runtime Directives (rd.xml) Configuration File Reference](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md). Доступны два средства устранения неполадок, которые предоставляют соответствующие записи для файла директив времени выполнения, устраняющие исключения [MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md) и [MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md) .  
  
-   [Средство устранения неполадок MissingMetadataException](https://dotnet.github.io/native/troubleshooter/type.html) для типов.  
  
-   [Средство устранения неполадок MissingMetadataException](https://dotnet.github.io/native/troubleshooter/method.html) для методов.  
  
> [!NOTE]
>  Этот справочник документирует три типа исключений, которые являются уникальными для [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Справочную документацию по основному API отражения для .NET Framework см. в разделе [Пространства имен System.Reflection](https://msdn.microsoft.com/library/gg145033.aspx). Справочную документацию по основному API взаимодействия для .NET Framework см. в разделе <xref:System.Runtime.InteropServices>.  
  
## <a name="systemreflection-namespace"></a>Пространства имен System.Reflection  
 Пространство имен <xref:System.Reflection> содержит базовые типы, используемые для отражения в платформе .NET Framework. Для [!INCLUDE[net_native](../../../includes/net-native-md.md)], оно также включает два новых типа исключений:  
  
|Класс|Описание|  
|-----------|-----------------|  
|[MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md)|Исключение, возникающее при использовании отражения для извлечения метаданных, которые не существуют.|  
|[MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)|Исключение возникает, когда метаданные для типа или члена типа доступны, но его реализация была удалена.|  
  
 Для получения сведений о других типов из этого пространства имен см. страницы справочника <xref:System.Reflection> в наборе документации платформы .NET Framework.  
  
## <a name="systemruntimecompilerservices-namespace"></a>Пространство имен System.Runtime.CompilerServices  
 Пространство имен <xref:System.Runtime.CompilerServices> содержит типы, создаваемые для пользователя компиляторами языка. Для [!INCLUDE[net_native](../../../includes/net-native-md.md)], оно также включает два новых типа исключений:  
  
|Класс|Описание|  
|-----------|-----------------|  
|[MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)|Исключение, которое возникает, когда вызывается ручной метод маршалинга, но не найдены метаданные для типа в ходе статического анализа или в файле директив среды выполнения.|  
  
 Для получения сведений о других типов из этого пространства имен см. страницы справочника <xref:System.Runtime.CompilerServices> в наборе документации платформы .NET Framework.  
  
## <a name="see-also"></a>См. также  
 [Класс MissingInteropDataException](../../../docs/framework/net-native/missinginteropdataexception-class-net-native.md)  
 [Класс MissingMetadataException](../../../docs/framework/net-native/missingmetadataexception-class-net-native.md)  
 [Класс MissingRuntimeArtifactException](../../../docs/framework/net-native/missingruntimeartifactexception-class-net-native.md)  
 [Начало работы](../../../docs/framework/net-native/getting-started-with-net-native.md)
