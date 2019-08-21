---
title: Обзор пошаговых руководств и технических описаний по началу работы
description: Модернизировать существующих приложений .NET с помощью Azure Cloud and Windows Containers | Обзор пошаговых руководств и руководства по началу работы
ms.date: 04/28/2018
ms.openlocfilehash: 81f7d9fbf596a23b83e2dc9251788b33a8817e16
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577857"
---
# <a name="walkthroughs-and-technical-get-started-overview"></a>Обзор пошаговых руководств и технических описаний по началу работы

Чтобы ограничить размер электронной книги, дополнительная техническая документация и все пошаговые руководства были сделаны доступными в репозитории GitHub. В интерактивной серии пошаговых руководств, описанных в этой главе, описывается пошаговая Настройка нескольких сред, основанных на контейнерах Windows, и развертывание в Azure.

В следующих разделах объясняется, что такое пошаговое руководство, его цели и концепция высокого уровня, а также приводится схема связанных задач. Пошаговые руководства можно получить в вики-сайте репозитория GitHub *eShopModernizing* Apps по <https://github.com/dotnet-architecture/eShopModernizing/wiki>адресу.

## <a name="technical-walkthrough-list"></a>Список технических пошаговых руководств

Приведенные ниже пошаговые руководства по началу работы предоставляют единообразные и исчерпывающие технические рекомендации для примеров приложений, которые можно передвигать и перемещать с помощью контейнеров, а затем переместить с помощью нескольких вариантов развертывания в Azure.

В каждом из следующих пошаговых руководств используются новые примеры приложений Ешоплегаци и eShopModernizing, которые доступны на сайте GitHub <https://github.com/dotnet-architecture/eShopModernizing>по адресу.

- **Обзор устаревших приложений Ешоп (базовые приложения для модернизировать)**

- **Контейнеризовать существующих веб-приложений ASP.NET (WebForms & MVC) с контейнерами Windows**

- **Контейнеризовать существующие службы WCF (N-уровневые приложения) с контейнерами Windows**

- **Развертывание приложения на основе контейнеров Windows на виртуальных машинах Azure**

- **Развертывание приложений на основе контейнеров Windows в Kubernetes в службе контейнеров Azure**

## <a name="walkthrough-1-tour-of-eshop-legacy-apps"></a>Пошаговое руководство 1. Обзор устаревших приложений Ешоп

### <a name="technical-walkthrough-availability"></a>Техническое руководство по доступности

Полное техническое руководство доступно на вики-сайте репозитория eShopModernizing GitHub:

[Пошаговые руководства по eShopModernizing wiki](https://github.com/dotnet-architecture/eShopModernizing/wiki)

### <a name="overview"></a>Обзор

В этом пошаговом руководстве можно изучить первоначальную реализацию трех примеров устаревших приложений. Первые два примера веб-приложений имеют монолитную архитектуру и созданы с помощью классической ASP.NET. Одно приложение основано на ASP.NET 4. x MVC; второе приложение основано на веб-формах ASP.NET 4. x.
Третье приложение — это 3-уровневое приложение, состоящее из клиентского приложения WinForms и службы [Windows Communication Foundation (WCF)](../../framework/wcf/whats-wcf.md) на стороне сервера.

Все эти приложения доступны в репозитории [EShopModernizing GitHub](https://github.com/dotnet-architecture/eShopModernizing).

### <a name="goals"></a>Цели

Основной целью этого пошагового руководства является простое знакомство с этими приложениями, а также с их кодом и конфигурацией. Можно настроить приложения таким образом, чтобы они создавали и использовали фиктивные данные без использования базы данных SQL в целях тестирования. Эта необязательная конфигурация основана на внедрении зависимостей в несвязанном виде.

### <a name="scenario-1-aspnet-web-apps"></a>Сценарий 1. Веб-приложения ASP.NET

На рисунке ниже показан простой сценарий исходных веб-приложений ASP.NET прежних версий.

![Простой сценарий архитектуры исходных веб-приложений ASP.NET прежних версий](./media/image5-1.png)

С точки зрения бизнес-домена оба приложения предлагают одни и те же функции управления каталогом. Участники группы Ешоп Enterprise будут использовать приложение для просмотра и редактирования каталога продуктов.

На следующем рисунке показаны первоначальные снимки экрана приложения.

![Приложения веб-форм ASP.NET MVC и ASP.NET (существующие и устаревшие технологии)](./media/image5-2.png)

Зависимости в ASP.NET 4. x или более ранних версиях (для MVC или для веб-форм) означает, что эти приложения не будут работать в .NET Core, если код не будет полностью переписан с помощью ASP.NET Core MVC.

### <a name="scenario-2-wcf-service-and-winforms-client-app-3-tier-app"></a>Сценарий 2. Служба WCF и клиентское приложение WinForms (3-уровневое приложение)

На рисунке ниже показан простой сценарий исходного приложения из трех уровней.

![Простой сценарий архитектуры исходного приложения в 3-уровневой версии с помощью службы WCF и клиентского приложения WinForms](./media/image5-1.5.png)

### <a name="benefits"></a>Преимущества

Преимущества этого пошагового руководства просты: Ознакомьтесь с кодом и начальными приложениями.

### <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:

- [Обзор по базовым ASP.NET MVC и веб-формам "устаревшие" приложения](https://github.com/dotnet-architecture/eShopModernizing/wiki/01.-Tour-on-the-ASP.NET-MVC-and-WebForms-apps-implementation-code)
- [Обзор базовых служб WCF и WinForms (3-уровневого) приложения "Legacy"](https://github.com/dotnet-architecture/eShopModernizing/wiki/21.-Tour-on-the-WCF-service-and-WinForms-apps)

## <a name="walkthrough-2-containerize-your-existing-net-applications-with-windows-containers"></a>Пошаговое руководство 2. Контейнеризовать существующие приложения .NET с контейнерами Windows

### <a name="overview"></a>Обзор

Используйте контейнеры Windows для улучшения развертывания существующих приложений .NET, например, на основе MVC, веб-форм или WCF, в рабочей среде, разработке и тестировании.

### <a name="goals"></a>Цели

Цель этого пошагового руководства — продемонстрировать несколько вариантов для контейнеризация существующего приложения .NET Framework. Можно выполнить следующие действия:

- Контейнеризовать приложение с помощью [средств Visual studio 2017 для DOCKER](/aspnet/core/host-and-deploy/docker/visual-studio-tools-for-docker) (visual Studio 2017 или более поздних версий).

- Контейнеризовать приложение, добавив [Dockerfile](https://docs.docker.com/engine/reference/builder/)вручную, а затем используя [DOCKER CLI](https://docs.docker.com/engine/reference/commandline/cli/).

- Контейнеризовать приложение с помощью средства [Img2Docker](https://github.com/docker/communitytools-image2docker-win) (средство с открытым исходным кодом из DOCKER).

В этом пошаговом руководстве рассматривается подход к использованию средств Visual Studio 2017 для DOCKER, но два других подхода довольно похожи в отношении использования файлы dockerfile.

### <a name="scenario-1-containerized-aspnet-web-apps"></a>Сценарий 1. Контейнерные веб-приложения ASP.NET

На рисунке ниже показан сценарий для контейнерных Ешоп устаревших приложений веб-приложений.

![Упрощенная схема использования контейнерных ASP.NET приложений в среде разработки](./media/image5-3.png)

### <a name="scenario-2-containerized-wcf-service"></a>Сценарий 2. Контейнерная служба WCF

На рисунке ниже показан сценарий для 3-уровневого приложения с контейнерной службой WCF.

![Упрощенная схема работы контейнерной службы WCF в среде разработки](./media/image5-3.5.png)

### <a name="benefits"></a>Преимущества

Выполнение монолитного приложения в контейнере имеет свои преимущества. Сначала необходимо создать образ для приложения. С этого момента каждое развертывание выполняется в одной среде. Каждый контейнер использует одну и ту же версию операционной системы, имеет одинаковую версию установленных зависимостей, использует одну и ту же версию .NET Framework и создается с помощью того же процесса. По сути, вы управляете зависимостями приложения с помощью образа DOCKER. Зависимости передаются вместе с приложением при развертывании контейнеров.

Дополнительное преимущество заключается в том, что разработчики могут запускать приложение в единообразной среде, предоставляемой контейнерами Windows. Проблемы, возникающие только с определенными версиями, можно сразу же получить, а не отображая в промежуточной или рабочей среде. Различия в средах разработки, которые используются членами группы разработки, меньше, когда приложения работают в контейнерах.

Контейнерные приложения также имеют кривую горизонтального масштабирования Flatter. Контейнерные приложения позволяют использовать больше экземпляров приложений и служб (на основе контейнеров) на ВИРТУАЛЬНОЙ машине или физическом компьютере по сравнению с обычными развертываниями приложений на компьютере. Это преобразуется в более высокую плотность и меньшее количество требуемых ресурсов, особенно при использовании оркестрации, например Kubernetes.

В идеале в идеальном случае не требуется вносить изменения в код приложения (C\#). В большинстве случаев требуются только файлы метаданных развертывания DOCKER (файлы файлы dockerfile и Docker Compose).

### <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:

- [Как контейнеризовать веб-приложения .NET Framework с помощью контейнеров Windows и DOCKER](https://github.com/dotnet-architecture/eShopModernizing/wiki/02.-How-to-containerize-the-.NET-Framework-web-apps-with-Windows-Containers-and-Docker)
- [Добавление поддержки DOCKER в службу WCF](https://github.com/dotnet-architecture/eShopModernizing/wiki/22.-Adding-Docker-Support)

## <a name="walkthrough-3-deploy-your-windows-containers-based-app-to-azure-vms"></a>Пошаговое руководство 3. Развертывание приложения на основе контейнеров Windows на виртуальных машинах Azure

### <a name="technical-walkthrough-availability"></a>Техническое руководство по доступности

Полное техническое руководство доступно на вики-сайте репозитория eShopModernizing GitHub:<https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

### <a name="overview"></a>Обзор

Развертывание на узле DOCKER на виртуальной машине Windows Server 2016 (ВМ) в Azure позволяет быстро настроить среды разработки, тестирования и промежуточного хранения. Она также позволяет тестерам или бизнес-пользователям часто проверять приложение. Виртуальные машины также могут быть допустимыми рабочими средами "инфраструктура как услуга" (IaaS).

### <a name="goals"></a>Цели

Цель этого пошагового руководства — продемонстрировать несколько вариантов, которые вы используете при развертывании контейнеров Windows на виртуальных машинах Azure, основанных на Windows Server 2016 или более поздних версиях.

### <a name="scenarios"></a>Сценарии

В этом пошаговом руководстве рассматривается несколько сценариев.

#### <a name="scenario-a-deploy-to-an-azure-vm-from-a-dev-pc-through-docker-engine-connection"></a>Сценарий а. Развертывание на виртуальной машине Azure с компьютера для разработки с помощью подключения к подсистеме DOCKER

![Развертывание на виртуальной машине Azure с компьютера для разработки через подключение к подсистеме DOCKER](./media/image5-4.png)

**Рис. 5-4.** Развертывание на виртуальной машине Azure с компьютера для разработки через подключение к подсистеме DOCKER

#### <a name="scenario-b-deploy-to-an-azure-vm-through-a-docker-registry"></a>Сценарий б. Развертывание на виртуальной машине Azure с помощью реестра DOCKER

![Развертывание на виртуальной машине Azure с помощью реестра DOCKER](./media/image5-5.png)

**Рис. 5-5.** Развертывание на виртуальной машине Azure с помощью реестра DOCKER

#### <a name="scenario-c-deploy-to-an-azure-vm-from-cicd-pipelines-in-azure-devops-services"></a>Сценарий в: Развертывание в виртуальной машине Azure из конвейеров CI/CD в Azure DevOps Services

![Развертывание в виртуальной машине Azure из конвейеров CI/CD в Azure DevOps Services](./media/image5-6.png)

**Рис. 5-6**. Развертывание в виртуальной машине Azure из конвейеров CI/CD в Azure DevOps Services

### <a name="azure-vms-for-windows-containers"></a>Виртуальные машины Azure для контейнеров Windows

Виртуальные машины Azure для контейнеров Windows — это виртуальные машины на основе Windows Server 2016, Windows 10 или более поздних версий с установленным подсистемой DOCKER. В большинстве случаев Windows Server 2016 используется на виртуальных машинах Azure.

В настоящее время Azure предоставляет виртуальную машину под названием **Windows Server 2016 с контейнерами**. Эту виртуальную машину можно использовать для использования новой функции контейнера Windows Server с Windows Server Core или Windows Nano Server. Образы ОС контейнера устанавливаются, а затем виртуальная машина готова к использованию с DOCKER.

### <a name="benefits"></a>Преимущества

Несмотря на то, что контейнеры Windows можно развертывать на локальных виртуальных машинах Windows Server 2016, при развертывании в Azure вы получаете более простой способ начать работу, используя готовые к использованию виртуальные машины контейнера Windows Server. Вы также получаете общее сетевое расположение, доступное для инженеров-тестировщиков, и автоматическое масштабирование с помощью масштабируемых наборов виртуальных машин Azure.

### <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/06.-Deploying-your-Windows-Containers-based-app-into-Azure-VMs-(Including-CI-CD)>

## <a name="walkthrough-4-deploy-your-windows-containers-based-apps-to-azure-container-instances-aci"></a>Пошаговое руководство 4. Развертывание приложений на основе контейнеров Windows в службе "экземпляры контейнеров Azure" (ACI)

### <a name="technical-walkthrough-availability"></a>Техническое руководство по доступности

Полное техническое руководство доступно на вики-сайте репозитория eShopModernizing GitHub:

[Развертывание приложений в ACI (службы "экземпляры контейнеров Azure")](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

### <a name="overview"></a>Обзор

Служба " [экземпляры контейнеров Azure" (ACI)](https://docs.microsoft.com/azure/container-instances/) — это самый быстрый способ использовать среду разработки, тестирования и промежуточного хранения контейнеров, где можно развернуть отдельные экземпляры контейнеров.

### <a name="goals"></a>Цели

В этом пошаговом руководстве показаны основные сценарии развертывания контейнеров Windows в службе "экземпляры контейнеров Azure" (ACI), а также способы развертывания приложений eShopModernizing в ACI.

### <a name="scenarios"></a>Сценарии

В ACI могут быть варианты развертывания приложений eShopModernizing, например развертывание только одного или всех приложений (приложение MVC, веб-формы или служба WCF). В приведенном ниже сценарии можно увидеть приложение ASP.NET MVC и контейнер SQL Server, развернутые в виде контейнеров в ACI (экземпляры контейнеров Azure).

![Развертывание в ACI из среды разработки](./media/image5-3.5.6.png)

### <a name="benefits"></a>Преимущества

Служба "экземпляры контейнеров Azure" упрощает создание контейнеров DOCKER в Azure и управление ими без необходимости подготавливать виртуальные машины или применять службу более высокого уровня. С помощью ACI можно напрямую развернуть контейнер Windows в Azure и предоставить его в Интернете с полным доменным именем (FQDN) в течение нескольких секунд (при условии, что образ контейнера Windows готов в реестре DOCKER, например в центре DOCKER или контейнере Azure). Реестр).

### <a name="considerations"></a>Рекомендации

Развертывание контейнеров Windows с полным .NET Framework, ASP.NET или SQL Server в службе "экземпляры контейнеров Azure" (ACI) не так быстро, как развертывание на обычном узле DOCKER (например, Windows Server 2016 с контейнерами Windows), так как образ DOCKER должен быть Загрузка (извлекаются из реестра DOCKER) каждый раз и размеры образа контейнера SQL (15,1 ГБ) и образа контейнера ASP.NET (13,9 ГБ) значительно велики, однако это гораздо дешевле, чем поддержание собственного узла DOCKER (постоянно в интерактивном виде). Windows Server 2016 с виртуальной машиной контейнеров Windows в Azure) не может упомянуть о всей Orchestrator, например Kubernetes в Azure (AKS), что, с другой стороны, отлично подходит для рабочих развертываний.

Как основное заключение, использование службы "экземпляры контейнеров Azure" является очень привлекательным вариантом для сценариев разработки и тестирования, а также для конвейеров CI/CD.

## <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:

[https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances)](https://github.com/dotnet-architecture/eShopModernizing/wiki/05.-Deploying-the-Apps-to-ACI-(Azure-Container-Instances))

## <a name="walkthrough-5-deploy-your-windows-containers-based-apps-to-kubernetes-in-azure-container-service"></a>Пошаговое руководство 5. Развертывание приложений на основе контейнеров Windows в Kubernetes в службе контейнеров Azure

### <a name="technical-walkthrough-availability"></a>Техническое руководство по доступности

Полное техническое руководство доступно на вики-сайте репозитория eShopModernizing GitHub:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

### <a name="overview"></a>Обзор

Приложение, основанное на контейнерах Windows, будет быстро использовать платформы, перенося их из виртуальных машин IaaS в другую систему. Это необходимо для простого обеспечения высокой масштабируемости и улучшенной масштабируемости, а для значительного улучшения автоматизированных развертываний и управления версиями. Эти цели можно достичь с помощью Orchestrator [Kubernetes](https://kubernetes.io/), доступного в [службе контейнеров Azure](https://azure.microsoft.com/services/container-service/).

### <a name="goals"></a>Цели

Цель этого пошагового руководства — узнать, как развернуть приложение на основе контейнера Windows в Kubernetes (другое название — *K8s*) в службе контейнеров Azure. Развертывание в Kubernetes с нуля состоит из двух этапов:

1. Развертывание кластера Kubernetes в службе контейнеров Azure.

2. Разверните приложение и связанные ресурсы в кластере Kubernetes.

### <a name="scenarios"></a>Сценарии

#### <a name="scenario-a-deploy-directly-to-a-kubernetes-cluster-from-a-dev-environment"></a>Сценарий а. Развертывание непосредственно в кластере Kubernetes из среды разработки

![Развертывание непосредственно в кластере Kubernetes из среды разработки](./media/image5-7.png)

**Рис. 5-7.** Развертывание непосредственно в кластере Kubernetes из среды разработки

#### <a name="scenario-b-deploy-to-a-kubernetes-cluster-from-cicd-pipelines-in-azure-devops-services"></a>Сценарий б. Развертывание в кластер Kubernetes из конвейеров CI/CD в Azure DevOps Services

![Развертывание в кластер Kubernetes из конвейеров CI/CD в Azure DevOps Services](./media/image5-8.png)

**Рис. 5-8.** Развертывание в кластер Kubernetes из конвейеров CI/CD в Azure DevOps Services

### <a name="benefits"></a>Преимущества

Развертывание в кластер в Kubernetes имеет множество преимуществ. Самое главное преимущество заключается в том, что вы получаете готовую среду, в которой можно масштабировать приложение на основе количества экземпляров контейнеров, которые вы хотите использовать (внутренняя масштабируемость в существующих узлах), и в зависимости от количества узлов или виртуальных машин в кластере ( Глобальная масштабируемость кластера).

Служба контейнеров Azure оптимизирует популярные средства и технологии с открытым кодом специально для Azure. Вы получаете открытое решение, которое предлагает переносимость для контейнеров и для конфигурации приложения. Вы выбрали размер, число узлов, а служба Orchestrator Tools-Container Service обрабатывает все остальное.

С помощью Kubernetes разработчики могут подумать о физических и виртуальных машинах, чтобы спланировать инфраструктуру, основанную на контейнерах, которая упрощает следующие возможности:

- Приложения, основанные на нескольких контейнерах

- Репликация экземпляров контейнеров и горизонтальное Автомасштабирование

- Именование и обнаружение (например, внутренняя служба DNS)

- Балансировка нагрузки

- Последовательные обновления

- Распространение секретов

- Проверки работоспособности приложений

## <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:<https://github.com/dotnet-architecture/eShopModernizing/wiki/04.-How-to-deploy-your-Windows-Containers-based-apps-into-Kubernetes-in-Azure-Container-Service-(Including-CI-CD)>

## <a name="walkthrough-6-deploy-your-windows-containers-based-apps-to-azure-app-service-for-containers"></a>Пошаговое руководство 6. Развертывание приложений на основе контейнеров Windows в службе приложений Azure для контейнеров

### <a name="technical-walkthrough-availability"></a>Техническое руководство по доступности

Полное техническое руководство доступно на вики-сайте репозитория eShopModernizing GitHub:

<https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

### <a name="overview"></a>Обзор

Простое контейнерное приложение, использующее контейнеры Windows, можно легко развернуть в службе приложений Azure для контейнеров. Это рекомендуемый подход для большинства приложений на основе контейнеров Windows.

### <a name="goals"></a>Цели

Цель этого пошагового руководства — узнать, как развернуть приложение на основе контейнера Windows в службе приложений Azure для контейнеров из реестра (DOCKER HUB или реестра контейнеров Azure).

### <a name="scenario"></a>Сценарий

![Развертывание приложения на основе контейнера Windows в службе приложений Azure для контейнеров](./media/image5-11.png)

### <a name="benefits"></a>Преимущества

Развертывание в службе приложений Azure для контейнеров предоставляет преимущества контейнеров, связанных с преимуществами PaaS службы приложений Azure. Службу приложений можно легко масштабировать как по вертикали, так и по горизонтали. ее можно настроить для автоматического масштабирования в соответствии с изменяющимися потребностями. Обновления могут выполняться с нулевым временем простоя и конфигурацией непрерывного развертывания из реестра.

## <a name="next-steps"></a>Следующие шаги

Подробное изучение этого содержимого на вики-сайте GitHub:<https://github.com/dotnet-architecture/eShopModernizing/wiki/Deploy-Windows-Container-to-Azure-App-Service>

> [!div class="step-by-step"]
> [Назад](modernize-existing-apps-to-cloud-optimized/migrate-to-hybrid-cloud-scenarios.md)
> [Вперед](conclusions.md)