---
title: Балансировка нагрузки gRPC-gRPC для разработчиков WCF
description: Выбор подсистемы балансировки нагрузки для работы со службами gRPC Services.
ms.date: 09/02/2019
ms.openlocfilehash: 215c0983146bbf9168f01956d64733f80cea6faf
ms.sourcegitcommit: 5fb5b6520b06d7f5e6131ec2ad854da302a28f2e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/03/2019
ms.locfileid: "74711166"
---
# <a name="load-balancing-grpc"></a>GRPC балансировки нагрузки

Типичное развертывание приложения gRPC включает ряд идентичных экземпляров службы, обеспечивая устойчивость и горизонтальную масштабируемость. Балансировка нагрузки распределяет входящие запросы между этими экземплярами, чтобы обеспечить полное использование всех доступных ресурсов. Чтобы обеспечить невидимость этой балансировки нагрузки для клиента, обычно используется сервер балансировщика нагрузки прокси-сервера для обработки запросов от клиентов и их маршрутизации к экземплярам серверной части.

Подсистемы балансировки нагрузки классифицируются в соответствии с *уровнем* , с которым они работают. Подсистемы балансировки нагрузки уровня 4 работают на *транспортном* уровне, например с сокетами TCP, соединениями и пакетами. Подсистемы балансировки нагрузки уровня 7 работают на уровне *приложения* , специально обрабатывая запросы HTTP/2 для приложений gRPC.

## <a name="l4-load-balancers"></a>Подсистемы балансировки нагрузки на уровне 4

Балансировщик нагрузки уровня 4 принимает запрос TCP-соединения от клиента, открывает другое соединение с одним из внутренних экземпляров и копирует данные между двумя соединениями без реальной обработки. Уровень 4 обеспечивает высокую производительность и низкую задержку, но очень мало средств управления и анализа. Пока клиент остается открытым, все запросы будут направлены на один и тот же экземпляр серверной части.

 [Azure Load Balancer](https://azure.microsoft.com/services/load-balancer/) является примером балансировщика нагрузки на уровне 4.

## <a name="l7-load-balancers"></a>Подсистемы балансировки нагрузки уровня 7

Балансировщик нагрузки уровня "на уровне 7" анализирует входящие запросы HTTP/2 и передает их на экземпляры серверной части по запросу, независимо от того, как долго соединение удерживает клиент.

Примеры подсистем балансировки нагрузки уровня 7:

- [NGINX](https://www.nginx.com/)
- [HAProxy](https://www.haproxy.com/)
- [траефик](https://traefik.io/)

Как правило, подсистемы балансировки нагрузки уровня "на уровне 7" являются лучшим выбором для gRPC и других приложений HTTP/2 (и для приложений HTTP, как правило, на самом деле). Подсистемы балансировки нагрузки уровня 4 будут *работать* с gRPC приложениями, но они особенно полезны, когда важны низкая задержка и низкая нагрузка.

> [!IMPORTANT]
> На момент написания этой статьи некоторые подсистемы балансировки нагрузки уровня 7 не поддерживают все части спецификации HTTP/2, необходимые службам gRPC Services, например конечные заголовки.

Если вы используете TLS-шифрование, подсистемы балансировки нагрузки могут завершить TLS-подключение и передать незашифрованные запросы серверному приложению или передать зашифрованный запрос вместе. В любом случае балансировщик нагрузки должен быть настроен с помощью открытого и закрытого ключей сервера, чтобы можно было расшифровывать запросы на обработку.

См. документацию по предпочтительной подсистеме балансировки нагрузки, чтобы узнать, как настроить его для обработки запросов HTTP/2 к серверным службам.

## <a name="load-balancing-within-kubernetes"></a>Балансировка нагрузки в Kubernetes

Описание балансировки нагрузки между внутренними службами в Kubernetes см. в [разделе о](service-mesh.md) связях между службами.

>[!div class="step-by-step"]
>[Назад](service-mesh.md)
>[Вперед](application-performance-management.md)