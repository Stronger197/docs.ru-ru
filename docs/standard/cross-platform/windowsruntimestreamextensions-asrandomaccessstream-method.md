---
title: Метод WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream)
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
api_name:
- System.IO.WindowsRuntimeStreamExtensions.AsRandomAccessStream
api_location:
- System.Runtime.WindowsRuntime.dll
ms.assetid: dcc72283-caed-49ee-b45d-ccaf94e97129
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 8935a8c282bbe812ad76ac6d4228c38ab12626a4
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/08/2018
ms.locfileid: "44193592"
---
# <a name="windowsruntimestreamextensionsasrandomaccessstreamsystemiostream-method"></a>Метод WindowsRuntimeStreamExtensions.AsRandomAccessStream(System.IO.Stream)

[Поддерживается в .NET Framework 4.5.1 и более поздних версиях.]

Преобразует заданный поток в поток прямого доступа.

**Пространство имен:** <xref:System.IO?displayProperty=nameWithType> 
 **сборки:** System.Runtime.WindowsRuntime (в System.Runtime.WindowsRuntime.dll)

## <a name="syntax"></a>Синтаксис

```csharp
[CLSCompliantAttribute(false)]
public static IRandomAccessStream AsRandomAccessStream(Stream stream)
```

```vb
'Declaration
<ExtensionAttribute> _
<CLSCompliantAttribute(False)> _
Public Shared Function AsRandomAccessStream ( _
        stream As Stream) As IRandomAccessStream
```

## <a name="parameters"></a>Параметры

`stream`

Тип: <xref:System.IO.Stream?displayProperty=nameWithType>  
Поток для преобразования.

## <a name="return-value"></a>Возвращаемое значение

Тип: <xref:Windows.Storage.Streams.RandomAccessStream>  
Объект [!INCLUDE[wrt](../../../includes/wrt-md.md)] поток прямого доступа, которая представляет преобразованный поток.

## <a name="exceptions"></a>Исключения

|Исключение|Условие|
|---------------|---------------|
|<xref:System.NotSupportedException>|Преобразуемый поток не поддерживает поиск.|

## <a name="remarks"></a>Примечания

Этот метод расширения доступен только при разработке приложений Магазина Windows. Этот метод обеспечивает удобный способ работы с потоками в приложениях Магазина Windows. Поток .NET Framework, который нужно преобразовать, должен поддерживать поиск. Дополнительные сведения см. в описании метода <xref:System.IO.Stream.Seek%2A?displayProperty=nameWithType>.

> [!IMPORTANT]
> Этот API поддерживается в платформе .NET Framework 4.5.1 и более поздних версиях, но не в версии 4.5.

## <a name="version-information"></a>Сведения о версии

**.NET для приложений Windows Store**

Поддерживается в Windows 8.1

## <a name="see-also"></a>См. также

-[System.IO.WindowsRuntimeStreamExtensions](https://msdn.microsoft.com/library/system.io.windowsruntimestreamextensions(v=vs.110).aspx)
-[как: преобразование между потоками .NET Framework и потоками среды выполнения Windows](../io/how-to-convert-between-dotnet-streams-and-winrt-streams.md)
