---
title: Выражение sub
ms.date: 07/20/2015
helpviewer_keywords:
- lambda expressions [Visual Basic], sub expression
- Sub Expression [Visual Basic]
- subroutines [Visual Basic], sub expressions
ms.assetid: 36b6bfd1-6539-4d8f-a5eb-6541a745ffde
ms.openlocfilehash: f862730220d0595faecaa915b1eaad2a3cdc0053
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84406320"
---
# <a name="sub-expression-visual-basic"></a>Часть выражения (Visual Basic)
Объявляет параметры и код, определяющие лямбда-выражение подпрограммы.  
  
## <a name="syntax"></a>Синтаксис  
  
```vb  
Sub ( [ parameterlist ] ) statement  
- or -  
Sub ( [ parameterlist ] )  
  [ statements ]  
End Sub  
```  
  
## <a name="parts"></a>Компоненты  
  
|Термин|Определение|  
|---|---|  
|`parameterlist`|Необязательный элемент. Список имен локальных переменных, представляющих параметры процедуры. Круглые скобки должны присутствовать, даже если список пуст. Дополнительные сведения см. в разделе [Parameter List](../statements/parameter-list.md).|  
|`statement`|Обязательный. Один оператор.|  
|`statements`|Обязательный. Список инструкций.|  
  
## <a name="remarks"></a>Комментарии  
 *Лямбда-выражение* — это подпрограммы без имени и выполняющая одну или несколько инструкций. Лямбда-выражение можно использовать в любом месте, где можно использовать тип делегата, за исключением того, что в качестве аргумента для `RemoveHandler` . Дополнительные сведения о делегатах и использовании лямбда-выражений с делегатами см. в разделе [оператор Delegate](../statements/delegate-statement.md) и [Преобразование неявного делегата](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md).  
  
## <a name="lambda-expression-syntax"></a>Синтаксис лямбда-выражений  
 Синтаксис лямбда-выражения напоминает стандартную подпрограммы. Различия заключаются в следующем.  
  
- Лямбда-выражение не имеет имени.  
  
- Лямбда-выражение не может иметь модификатор, например `Overloads` или `Overrides` .  
  
- Тело однострочного лямбда-выражения должно быть оператором, а не выражением. Тело может состоять из вызова подпроцедуры, но не вызова процедуры функции.  
  
- В лямбда-выражении либо все параметры должны иметь указанные типы данных, либо все параметры должны быть выведены.  
  
- Необязательные `ParamArray` Параметры и не допускаются в лямбда-выражениях.  
  
- Универсальные параметры не допускаются в лямбда-выражениях.  
  
## <a name="example"></a>Пример  
 Ниже приведен пример лямбда-выражения, записывающего значение в консоль. В примере показан синтаксис однострочного и многострочного лямбда-выражения для подпрограммы. Дополнительные примеры см. в разделе [лямбда-выражения](../../programming-guide/language-features/procedures/lambda-expressions.md).  
  
 [!code-vb[VbVbalrLambdas#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrLambdas/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>См. также раздел

- [Оператор Sub](../statements/sub-statement.md)
- [Лямбда-выражения](../../programming-guide/language-features/procedures/lambda-expressions.md)
- [Операторы и выражения](../../programming-guide/language-features/operators-and-expressions/index.md)
- [Операторы](../../programming-guide/language-features/statements.md)
- [Неявное преобразование делегата](../../programming-guide/language-features/delegates/relaxed-delegate-conversion.md)
