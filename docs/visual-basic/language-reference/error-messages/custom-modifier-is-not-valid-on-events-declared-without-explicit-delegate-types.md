---
title: Модификатор Custom недопустим для событий, объявленных без явных делегируемых типов
ms.date: 07/20/2015
f1_keywords:
- vbc31122
- bc31122
helpviewer_keywords:
- BC31122
ms.assetid: 6911f0d1-641a-473b-906d-8ee5681194be
ms.openlocfilehash: 0c5a4188fedf9685afdd1cde4c1de93a0b43b919
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409791"
---
# <a name="custom-modifier-is-not-valid-on-events-declared-without-explicit-delegate-types"></a>Модификатор Custom недопустим для событий, объявленных без явных делегируемых типов
В отличие от нестандартного события, `Custom Event` объявление требует наличия `As` предложения, следующего за именем события, которое явно указывает тип делегата для события.  
  
 Ненастраиваемые события могут быть определены с помощью предложения, `As` явного типа делегата или списка параметров, непосредственно следующего за именем события.  
  
 **Идентификатор ошибки:** BC31122  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1. Определите делегат с тем же списком параметров, что и пользовательское событие.  
  
     Например, если объект `Custom Event` был определен с помощью `Custom Event Test(ByVal sender As Object, ByVal i As Integer)` , соответствующий делегат будет выглядеть следующим образом.  
  
     [!code-vb[VbVbalrEventError#18](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#18)]  
  
2. Замените список параметров пользовательского события `As` предложением с указанием типа делегата.  
  
     Продолжая работу с примером, `Custom Event` объявление будет перезаписано следующим образом.  
  
     [!code-vb[VbVbalrEventError#19](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#19)]  
  
## <a name="example"></a>Пример  
 В этом примере объявляется `Custom Event` и указывается обязательное `As` предложение с типом делегата.  
  
 [!code-vb[VbVbalrEventError#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrEventError/VB/VbVbalrEventError.vb#2)]  
  
## <a name="see-also"></a>См. также раздел

- [Оператор Event](../statements/event-statement.md)
- [Оператор Delegate](../statements/delegate-statement.md)
- [События](../../programming-guide/language-features/events/index.md)
