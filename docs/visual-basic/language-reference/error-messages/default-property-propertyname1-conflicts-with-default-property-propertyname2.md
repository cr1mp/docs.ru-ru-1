---
title: Свойство <propertyname1>, используемое по умолчанию, конфликтует со свойством <propertyname2>, используемым по умолчанию в классе <classname>, и должно быть объявлено с ключевым словом Shadows
ms.date: 07/20/2015
f1_keywords:
- vbc40007
- bc40007
helpviewer_keywords:
- BC40007
ms.assetid: 692ccf76-5715-4f11-a972-84cf9de30bc1
ms.openlocfilehash: 37f98ce8120d5861552819690f9d5f22c9959a0e
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2020
ms.locfileid: "84409729"
---
# <a name="default-property-propertyname1-conflicts-with-default-property-propertyname2-in-classname-and-so-should-be-declared-shadows"></a>Свойство \<propertyname1>, используемое по умолчанию, конфликтует со свойством \<propertyname2>, используемым по умолчанию в классе \<classname>, и должно быть объявлено с ключевым словом Shadows
Свойство объявлено с тем же именем, что и у свойства, определенного в базовом классе. В этом случае свойство в этом классе должно скрывать свойство базового класса.  
  
 Это сообщение является предупреждением. `Shadows` подразумевается по умолчанию. Дополнительные сведения о сокрытии предупреждений и обработке предупреждений как ошибок см. в разделе [Configuring Warnings in Visual Basic](/visualstudio/ide/configuring-warnings-in-visual-basic).  
  
 **Идентификатор ошибки:** BC40007  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
- Добавьте `Shadows` ключевое слово в объявление или измените имя объявляемого свойства.  
  
## <a name="see-also"></a>См. также раздел

- [Shadows](../modifiers/shadows.md)
- [Сокрытие в Visual Basic](../../programming-guide/language-features/declared-elements/shadowing.md)
