---
title: Выполнение выборочных модульных тестов
description: Демонстрация использования выражения фильтра для выполнения выборочных модульных тестов с помощью команды dotnet test.
author: smadala
ms.author: mairaw
ms.date: 03/22/2017
ms.openlocfilehash: 428e31014f5d8d487deb7c4b4317ebcef13c294d
ms.sourcegitcommit: 2eceb05f1a5bb261291a1f6a91c5153727ac1c19
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/04/2018
ms.locfileid: "43517224"
---
# <a name="running-selective-unit-tests"></a>Выполнение выборочных модульных тестов

В следующих примерах используется `dotnet test`. Если вы используете `vstest.console.exe`, замените `--filter ` на `--testcasefilter:`.

## <a name="mstest"></a>MSTest

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace MSTestNamespace
{
    [TestClass]
    public class UnitTest1
    {
        [TestCategory("CategoryA")]
        [Priority(1)]
        [TestMethod]
        public void TestMethod1()
        {
        }

        [Priority(2)]
        [TestMethod]
        public void TestMethod2()
        {
        }
    }
}
```

| Выражение | Результат |
| ---------- | ------ |
| `dotnet test --filter Method` | Выполняет тесты, `FullyQualifiedName` которых содержит `Method`. Доступно в `vstest 15.1+`. |
| `dotnet test --filter Name~TestMethod1` | Выполняет тесты, имя которых содержит `TestMethod1`. |
| `dotnet test --filter ClassName=MSTestNamespace.UnitTest1` | Выполняет тесты, которые находятся в классе `MSTestNamespace.UnitTest1`.<br>**Примечание.** Значение `ClassName` должно иметь пространство имен, поэтому `ClassName=UnitTest1` не будет работать. |
| `dotnet test --filter FullyQualifiedName!=MSTestNamespace.UnitTest1.TestMethod1` | Выполняет все тесты, за исключением `MSTestNamespace.UnitTest1.TestMethod1`. |
| `dotnet test --filter TestCategory=CategoryA` | Выполняет тесты, которые помечены атрибутом `[TestCategory("CategoryA")]`. |
| `dotnet test --filter Priority=2` | Выполняет тесты, которые помечены атрибутом `[Priority(2)]`.<br>

**Использование условных операторов | и &amp;**

| Выражение | Результат |
| ---------- | ------ |
| <code>dotnet test --filter "FullyQualifiedName~UnitTest1&#124;TestCategory=CategoryA"</code> | Выполняет тесты, имеющие `UnitTest1` в `FullyQualifiedName` **или** `TestCategory` является `CategoryA`. |
| `dotnet test --filter "FullyQualifiedName~UnitTest1&TestCategory=CategoryA"` | Выполняет тесты, имеющие `UnitTest1` в `FullyQualifiedName` **и** `TestCategory` является `CategoryA`. |
| <code>dotnet test --filter "(FullyQualifiedName~UnitTest1&TestCategory=CategoryA)&#124;Priority=1"</code> | Выполняет тесты, в которых либо `FullyQualifiedName` содержит `UnitTest1` **и** `TestCategory` является `CategoryA`, **либо** `Priority` равно 1. |

## <a name="xunit"></a>xUnit

```csharp
using Xunit;

namespace XUnitNamespace
{
    public class TestClass1
    {
        [Trait("Category", "CategoryA")]
        [Trait("Priority", "1")]
        [Fact]
        public void Test1()
        {
        }

        [Trait("Priority", "2")]
        [Fact]
        public void Test2()
        {
        }
    }
}
```

| Выражение | Результат |
| ---------- | ------ |
| `dotnet test --filter DisplayName=XUnitNamespace.TestClass1.Test1` | Выполняет только один тест — `XUnitNamespace.TestClass1.Test1`. |
| `dotnet test --filter FullyQualifiedName!=XUnitNamespace.TestClass1.Test1` | Выполняет все тесты, за исключением `XUnitNamespace.TestClass1.Test1`. |
| `dotnet test --filter DisplayName~TestClass1` | Выполняет тесты, отображаемое имя которых содержит `TestClass1`. |

В примере кода определенные характеристики с ключами `Category` и `Priority` можно использовать для фильтрации.

| Выражение | Результат |
| ---------- | ------ |
| `dotnet test --filter XUnit` | Выполняет тесты, `FullyQualifiedName` которых содержит `XUnit`.  Доступно в `vstest 15.1+`. |
| `dotnet test --filter Category=CategoryA` | Выполняет тесты, имеющие `[Trait("Category", "CategoryA")]`. |

**Использование условных операторов | и &amp;**

| Выражение | Результат |
| ---------- | ------ |
| <code>dotnet test --filter "FullyQualifiedName~TestClass1&#124;Category=CategoryA"</code> | Выполняет тесты, имеющие `TestClass1` в `FullyQualifiedName` **или** `Category` является `CategoryA`. |
| `dotnet test --filter "FullyQualifiedName~TestClass1&Category=CategoryA"` | Выполняет тесты, имеющие `TestClass1` в `FullyQualifiedName` **или** `Category` является `CategoryA`. |
| <code>dotnet test --filter "(FullyQualifiedName~TestClass1&Category=CategoryA)&#124;Priority=1"</code> | Выполняет тесты, в которых либо `FullyQualifiedName` содержит `TestClass1` **и** `Category` является `CategoryA`, **либо** `Priority` равно 1. |

## <a name="nunit"></a>NUnit

```csharp
using NUnit.Framework;

namespace NUnitNamespace
{
    public class UnitTest1
    {
        [Category("CategoryA")]
        [Property("Priority", 1)]
        [Test]
        public void TestMethod1()
        {
        }

        [Property("Priority", 2)]
        [Test]
        public void TestMethod2()
        {
        }
    }
}
```

| Выражение | Результат |
| ---------- | ------ |
| `dotnet test --filter Method` | Выполняет тесты, `FullyQualifiedName` которых содержит `Method`. Доступно в `vstest 15.1+`. |
| `dotnet test --filter Name~TestMethod1` | Выполняет тесты, имя которых содержит `TestMethod1`. |
| `dotnet test --filter FullyQualifiedName~NUnitNamespace.UnitTest1` | Выполняет тесты, которые находятся в классе `NUnitNamespace.UnitTest1`.<br>
| `dotnet test --filter FullyQualifiedName!=NUnitNamespace.UnitTest1.TestMethod1` | Выполняет все тесты, за исключением `NUnitNamespace.UnitTest1.TestMethod1`. |
| `dotnet test --filter TestCategory=CategoryA` | Выполняет тесты, которые помечены атрибутом `[Category("CategoryA")]`. |
| `dotnet test --filter Priority=2` | Выполняет тесты, которые помечены атрибутом `[Priority(2)]`.<br>

**Использование условных операторов | и &amp;**

| Выражение | Результат |
| ---------- | ------ |
| <code>dotnet test --filter "FullyQualifiedName~UnitTest1&#124;TestCategory=CategoryA"</code> | Выполняет тесты, имеющие `UnitTest1` в `FullyQualifiedName` **или** `TestCategory` является `CategoryA`. |
| `dotnet test --filter "FullyQualifiedName~UnitTest1&TestCategory=CategoryA"` | Выполняет тесты, имеющие `UnitTest1` в `FullyQualifiedName` **и** `TestCategory` является `CategoryA`. |
| <code>dotnet test --filter "(FullyQualifiedName~UnitTest1&TestCategory=CategoryA)&#124;Priority=1"</code> | Выполняет тесты, в которых либо `FullyQualifiedName` содержит `UnitTest1` **и** `TestCategory` является `CategoryA`, **либо** `Priority` равно 1. |
