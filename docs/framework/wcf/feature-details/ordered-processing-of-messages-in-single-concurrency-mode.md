---
title: Упорядоченная обработка сообщений в режиме единого параллелизма
ms.date: 03/30/2017
ms.assetid: a90f5662-a796-46cd-ae33-30a4072838af
ms.openlocfilehash: baba75fe398d974f989acfda7ef7366986f6813b
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/09/2020
ms.locfileid: "84598740"
---
# <a name="ordered-processing-of-messages-in-single-concurrency-mode"></a>Упорядоченная обработка сообщений в режиме единого параллелизма
WCF не предоставляет никаких гарантий относительно порядка обработки сообщений, если только базовый канал не является сеансом.  Например, служба WCF, использующая Мсмкинпутчаннел, которая не является каналом с сеансом, не сможет обрабатывать сообщения по порядку. Существуют некоторые обстоятельства, в которых разработчику может потребоваться поведение при обработке заказа, но не нужно использовать сеансы. В этом разделе описано, как настроить такое поведение, когда служба запущена в режиме единого параллелизма.  
  
## <a name="in-order-message-processing"></a>Упорядоченная обработка сообщений  
 В <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> добавлен новый атрибут <xref:System.ServiceModel.ServiceBehaviorAttribute>. Если <xref:System.ServiceModel.ServiceBehaviorAttribute.EnsureOrderedDispatch%2A> задано значение true и <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> задается значение <xref:System.ServiceModel.ConcurrencyMode.Single>, сообщения, отправленные службе, будут обработаны по порядку. В следующем фрагменте кода показано, как задать эти атрибуты.  
  
```csharp
[ServiceBehavior(ConcurrencyMode = ConcurrencyMode.Single, EnsureOrderedDispatch = true )]  
    class Service : IService  
    {  
         // ...  
    }  
```  
  
 Если <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> имеет любое другое значение, выдается исключение <xref:System.InvalidOperationException>.  
  
## <a name="see-also"></a>Дополнительно

- [Сеансы, экземпляры и параллелизм](sessions-instancing-and-concurrency.md)
- [Параллелизм](../samples/concurrency.md)
