---
description: var. Справочник по C#
title: var. Справочник по C#
ms.date: 07/20/2015
f1_keywords:
- var
- var_CSharpKeyword
helpviewer_keywords:
- var keyword [C#]
ms.assetid: 0777850a-2691-4e3e-927f-0c850f5efe15
ms.openlocfilehash: 303a880a54a79e50515060e0ea28e8d021fa1b76
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/30/2020
ms.locfileid: "89141716"
---
# <a name="var-c-reference"></a>var (справочник по C#)

Начиная с Visual C# 3.0, переменные, объявленные в области действия метода, получают неявный "тип" `var`. Неявно типизированные локальные переменные является строго типизированными, как если бы вы объявили тип самостоятельно, однако его определяет компилятор. Следующие два объявления `i` функционально эквивалентны:

```csharp
var i = 10; // Implicitly typed.
int i = 10; // Explicitly typed.
```

Дополнительные сведения см. в разделах [Неявно типизированные локальные переменные](../../programming-guide/classes-and-structs/implicitly-typed-local-variables.md) и [Связи типов в операциях запроса LINQ](../../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).

> [!IMPORTANT]
> При использовании `var` с включенными ссылочными типами, допускающими значение NULL, всегда подразумевается ссылочный тип, допускающий значение NULL, даже если тип выражения не допускает значения NULL.

## <a name="example"></a>Пример

В следующем примере показаны два выражения запросов. В первом выражении использование `var` разрешено, но не является обязательным, поскольку тип результата запроса может быть задан явно как `IEnumerable<string>`. Однако во втором выражении благодаря `var` результат может быть коллекцией анонимных типов, и имя этого типа доступно только для компилятора. Использование `var` делает создание нового класса для результата необязательным. Обратите внимание на то, что во втором примере переменная итерации `foreach``item` также типизирована неявно.

[!code-csharp[csrefKeywordsTypes#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsTypes/CS/keywordsTypes.cs#18)]

## <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Неявно типизированные локальные переменные](../../programming-guide/classes-and-structs/implicitly-typed-local-variables.md)
