---
title: <exposedMethod>
ms.date: 03/30/2017
ms.assetid: 61c938cd-4ee9-4b06-ab28-922ef491ab11
ms.openlocfilehash: 46f2872fb289c2793c356ea179deb3ce52e6d65e
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/06/2020
ms.locfileid: "70855306"
---
# \<exposedMethod>
Представляет метод COM+, предоставляемый, когда интерфейс компонента COM+ предоставляется как веб-служба.  
  
[**\<configuration>**](../configuration-element.md)\
&nbsp;&nbsp;[**\<system.serviceModel>**](system-servicemodel.md)\
&nbsp;&nbsp;&nbsp;&nbsp;[**\<comContracts>**](comcontracts.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<comContract>**](comcontract.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[**\<exposedMethods>**](exposedmethods.md)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**\<exposedMethod>**  
  
## <a name="syntax"></a>Синтаксис  
  
```xml  
<comContracts>
  <comContract>
    <exposedMethods>
      <exposedMethod name="String" />
    </exposedMethods>
  </comContract>
</comContracts>
```  
  
## <a name="attributes-and-elements"></a>Атрибуты и элементы  
 В следующих разделах описаны атрибуты, дочерние и родительские элементы.  
  
### <a name="attributes"></a>Атрибуты  
  
|Атрибут|Описание|  
|---------------|-----------------|  
|name|Строка, которая содержит метод COM+, предоставляемый, когда интерфейс компонента COM+ предоставляется как веб-служба.|  
  
### <a name="child-elements"></a>Дочерние элементы  
 Отсутствует.  
  
### <a name="parent-elements"></a>Родительские элементы  
  
|Элемент|Описание|  
|-------------|-----------------|  
|[\<exposedMethods>](exposedmethods.md)|Коллекция [\<exposedMethod>](exposedmethod.md) элементов.|  
  
## <a name="remarks"></a>Примечания  
 Средство конфигурации интеграции COM+ (ComSvcConfig.exe) может применяться для добавления определенных методов COM-интерфейса для использования в созданном контракте службы.  
  
 Например, для добавления в созданный контракт службы трех именованных методов из COM-интерфейса `IFinances` компонента `ItemOrders`.Financial можно использовать приведенную ниже команду.  
  
 `ComSvcConfig.exe /i /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{TransferFunds,AddFunds,RemoveFunds} /hosting:complus`  
  
 При запуске файла ComSvcConfig. exe он создает следующий контракт службы, в котором перечислены упомянутые выше методы в качестве [\<exposedMethod>](exposedmethod.md) элементов.  
  
```xml  
<comContract contractType="{C551FBA9-E3AA-4272-8C2A-84BD8D290AC7}"
             name="IFinances"
             namespace="http://contoso.com/services/financial">
  <exposedMethod name="TransferFunds"/>
  <exposedMethod name="AddFunds"/>
  <exposedMethod name="RemoveFunds"/>
</comContract>
```  
  
 Во время инициализации службы среда выполнения пытается создать контракт службы, отражая и добавляя только методы, входящие в список [\<exposedMethod>](exposedmethod.md) элементов. Для каждого метода интерфейса, который не включен в контракт службы, создается трассировка.  
  
## <a name="see-also"></a>См. также

- <xref:System.ServiceModel.Configuration.ComMethodElementCollection>
- <xref:System.ServiceModel.Configuration.ComMethodElement>
- [\<comContracts>](comcontracts.md)
- [Интеграция с приложениями COM+](../../../wcf/feature-details/integrating-with-com-plus-applications.md)
- [Практическое руководство. Настройка параметров службы COM+](../../../wcf/feature-details/how-to-configure-com-service-settings.md)
