---
description: '#warning. Справочник по C#'
title: '#warning. Справочник по C#'
ms.date: 07/20/2015
f1_keywords:
- '#warning'
helpviewer_keywords:
- '#warning directive [C#]'
ms.assetid: e6fb496d-bb8b-4018-baf6-5b60a0c8902b
ms.openlocfilehash: ab2cc5120492fc2a4b94296eb85e563c0a1d5ad3
ms.sourcegitcommit: d579fb5e4b46745fd0f1f8874c94c6469ce58604
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/30/2020
ms.locfileid: "89137842"
---
# <a name="warning-c-reference"></a>#warning (справочник по C#)
`#warning` позволяет создать предупреждение компилятора [CS1030](../../misc/cs1030.md) первого уровня из определенного места в коде. Пример:  
  
```csharp
#warning Deprecated code in this method.  
```  
  
## <a name="remarks"></a>Remarks
 Как правило, `#warning` применяется в условной директиве. Кроме того, с помощью директивы [#error](./preprocessor-error.md) можно создать определяемую пользователем ошибку.  
  
## <a name="example"></a>Пример  

```csharp
// preprocessor_warning.cs  
// CS1030 expected  
#define DEBUG  
class MainClass
{  
    static void Main()
    {  
#if DEBUG  
#warning DEBUG is defined  
#endif  
    }  
}  
```  

## <a name="see-also"></a>См. также

- [Справочник по C#](../index.md)
- [Руководство по программированию на C#](../../programming-guide/index.md)
- [Директивы препроцессора C#](./index.md)
