---
title: Функция Dir должна первый раз вызываться с аргументом PathName
ms.date: 07/20/2015
f1_keywords:
- vbrDIR_IllegalCall
ms.assetid: 7b5d149f-be91-4ac3-8262-86a360894e7d
ms.openlocfilehash: d255b8dddd098835764f72b8a166eaa08b0353df
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/23/2019
ms.locfileid: "61803458"
---
# <a name="dir-function-must-first-be-called-with-a-pathname-argument"></a>Функция Dir должна первый раз вызываться с аргументом PathName
Исходный вызов `Dir` функция не поддерживает `PathName` аргумент. Первый вызов `Dir` должен включать `PathName`, но последующие вызовы `Dir` не обязательно должны включать параметры для извлечения следующего элемента.  
  
## <a name="to-correct-this-error"></a>Исправление ошибки  
  
1. Укажите `PathName` аргумента в вызове функции.  
  
## <a name="see-also"></a>См. также

- <xref:Microsoft.VisualBasic.FileSystem.Dir%2A>
