---
title: Перенос веб-приложения ASP.NET на виртуальную машину Azure
description: Узнайте, как перенести веб-приложение ASP.NET из локальной среды на виртуальную машину Azure.
ms.topic: how-to
ms.date: 06/20/2020
ms.openlocfilehash: 5ef340d020b72bebe46fe598fe68e7d02d0c0363
ms.sourcegitcommit: cb27c01a8b0b4630148374638aff4e2221f90b22
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/09/2020
ms.locfileid: "86174248"
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a>Перенос веб-приложения ASP.NET на виртуальную машину Azure

В этом документе приводятся общие сведения о том, как перенести веб-приложение ASP.NET из локальной среды на виртуальную машину Azure.

## <a name="quickstart"></a>Краткое руководство

Узнайте, как создать виртуальную машину и опубликовать на ней приложение: [Публикация на виртуальной машине Azure](https://tutorials.visualstudio.com/aspnet-vm/intro)

## <a name="get-started"></a>Приступая к работе

В этих руководствах показано, как создать (перенести) виртуальную машину и опубликовать на ней веб-приложение, а также как выполнить другие задачи, которые могут потребоваться для поддержки приложения в Azure.

- Создайте виртуальную машину в Azure для приложения ASP.NET, используя один из следующих вариантов:
  - [Создание виртуальной машины для приложений ASP.NET](https://go.microsoft.com/fwlink/?linkid=863237).
  - [Перенос существующей локальной виртуальной машины VMware](/azure/migrate/tutorial-migrate-vmware).
  - [Перенос существующей локальной виртуальной машины Hyper-V](/azure/migrate/tutorial-migrate-hyper-v).
- [Опубликуйте свое приложение с помощью Visual Studio](https://go.microsoft.com/fwlink/?linkid=863240).
- [Создайте защищенную виртуальную сеть для виртуальных машин](/azure/virtual-network/virtual-network-get-started-vnet-subnet).
- [Создайте конвейер непрерывной интеграции или непрерывного развертывания для приложения](/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups).
- [Перенесите приложение в масштабируемый набор виртуальных машин, чтобы обеспечить высокий уровень доступности и масштабируемость](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).

## <a name="considerations"></a>Особенности

### <a name="benefits"></a>Преимущества

Виртуальные машины предоставляют самый простой способ переноса приложения из локальной среды в облако. Они позволяют реплицировать ту среду, которую приложение использует локально, устраняя необходимость в обслуживании собственных центров обработки данных. Масштабируемые наборы виртуальных машин обеспечивают высокий уровень доступности и масштабируемость для приложений, выполняемых на виртуальных машинах.

### <a name="virtual-machine-size"></a>Размер виртуальной машины

Выберите размер и тип виртуальной машины, которые лучше всего оптимизированы для вашей рабочей нагрузки. Дополнительные сведения см. в статье [Размеры виртуальных машин Windows в Azure](/azure/virtual-machines/windows/sizes).

### <a name="maintenance"></a>Обслуживание

Как и с локальными компьютерами, вы несете ответственность за обслуживание и обновление виртуальной машины<sup>&#42;</sup>. Если приложение может выполняться в среде PaaS (платформа как услуга), например в [службе приложений Azure](/azure/app-service/) или в [контейнере](/azure/app-service/containers/), то необходимость в обслуживании устраняется.

*<sup>&#42;</sup>[Автоматическое обновление ОС для масштабируемых наборов виртуальных машин](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) сейчас доступно в виде предварительной версии.*

### <a name="virtual-networks"></a>Виртуальные сети

Виртуальные сети Azure позволяют выполнять следующие задачи:

- Создание управляемой гибридной инфраструктуры.
- Использование собственных IP-адресов и DNS-серверов.
- Создание изолированной и надежно защищенной среды для приложений.
- Подключение виртуальной машины к локальной сети с использованием одного из нескольких [вариантов подключения](/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti).
- Интеграция виртуальной машины с локальной сетью с помощью [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

Чтобы начать работу, ознакомьтесь с [документацией по виртуальным сетям](/azure/virtual-network/).

### <a name="active-directory"></a>Active Directory
Многие приложения используют Active Directory для проверки подлинности и управления удостоверениями.

- Azure AD Connect позволяет интегрировать локальные каталоги с Azure Active Directory. Чтобы приступить к работе, изучите статью [Интеграция локальных каталогов с Azure Active Directory](/azure/active-directory/connect/active-directory-aadconnect).
- Также и [ExpressRoute](https://azure.microsoft.com/services/expressroute/) позволяет приложению получить доступ к локальной службе Active Directory.

### <a name="sql-databases"></a>Базы данных SQL

Если приложение использует локальную базу данных, оно не сможет обращаться к ней по умолчанию. Вы можете сделать одно из двух:

- Настройте гибридную сеть, которая позволит вашему приложению получать доступ к базе данных, работающей локально.
- Перенесите базу данных в Azure. Дополнительные сведения см. в статье [Перенос базы данных SQL Server в Azure](sql.md).

### <a name="high-availability-and-scalability"></a>Высокий уровень доступности и масштабируемости

#### <a name="virtual-machine-scale-sets"></a>Масштабируемые наборы виртуальных машин Microsoft Azure
Если вам нужно обеспечить высокий уровень доступности и возможность масштабирования для приложения, перенесите образ виртуальной машины в масштабируемый набор виртуальных машин Azure, чтобы повысить уровень доступности и улучшить возможность масштабирования приложения. Масштабируемые наборы виртуальных машин позволяют использовать уже настроенную виртуальную машину или настроить конвейер сборки, чтобы создать образ с вашим приложением.

Чтобы приступить к работе, изучите статью [Развертывание приложения в масштабируемых наборах виртуальных машин](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).

#### <a name="centralized-logging"></a>Централизованное ведение журналов
Если приложение выполняется на нескольких экземплярах, рассмотрите возможность хранения журналов в централизованном расположении, например в [хранилище Azure](/azure/storage/).

## <a name="next-steps"></a>Следующие шаги

> [!div class="nextstepaction"]
> [Перенос базы данных SQL Server в Azure](sql.md)
