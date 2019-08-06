---
title: Что такое Docker?
description: Архитектура микрослужб .NET для упакованных в контейнеры приложений .NET | Что такое Docker?
ms.date: 08/31/2018
ms.openlocfilehash: 7f7844f51e96914c1432332d9b641ea65bf48f07
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/30/2019
ms.locfileid: "68674861"
---
# <a name="what-is-docker"></a><span data-ttu-id="9b66e-103">Что такое Docker?</span><span class="sxs-lookup"><span data-stu-id="9b66e-103">What is Docker?</span></span>

<span data-ttu-id="9b66e-104">[Docker](https://www.docker.com/) — это [проект с открытым исходным кодом](https://github.com/docker/docker) для автоматизации развертывания приложений в виде переносимых автономных контейнеров, выполняемых в облаке или локальной среде.</span><span class="sxs-lookup"><span data-stu-id="9b66e-104">[Docker](https://www.docker.com/) is an [open-source project](https://github.com/docker/docker) for automating the deployment of applications as portable, self-sufficient containers that can run on the cloud or on-premises.</span></span> <span data-ttu-id="9b66e-105">Одновременно с этим, Docker — это [компания](https://www.docker.com/), которая разрабатывает и продвигает эту технологию в сотрудничестве с поставщиками облачных служб, а также решений Linux и Windows, включая корпорацию Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9b66e-105">Docker is also a [company](https://www.docker.com/) that promotes and evolves this technology, working in collaboration with cloud, Linux, and Windows vendors, including Microsoft.</span></span>

![Контейнеры Docker могут работать в любой среде, например в локальном центре обработки данных, в службе стороннего поставщика или в облаке Azure.](./media/image2.png)

<span data-ttu-id="9b66e-107">**Рис. 2-2**.</span><span class="sxs-lookup"><span data-stu-id="9b66e-107">**Figure 2-2**.</span></span> <span data-ttu-id="9b66e-108">Docker развертывает контейнеры на всех уровнях гибридного облака</span><span class="sxs-lookup"><span data-stu-id="9b66e-108">Docker deploys containers at all layers of the hybrid cloud</span></span>

<span data-ttu-id="9b66e-109">Контейнеры образов Docker работают в исходном формате в Linux и Windows.</span><span class="sxs-lookup"><span data-stu-id="9b66e-109">Docker image containers can run natively on Linux and Windows.</span></span> <span data-ttu-id="9b66e-110">Но образы Windows будут выполняться только на узлах Windows, тогда как образы Linux — на узлах Linux или Windows (на данный момент с помощью виртуальной машины Linux Hyper-V). Термин "узлы" здесь означает физические серверы и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="9b66e-110">However, Windows images can run only on Windows hosts and Linux images can run on Linux hosts and Windows hosts (using a Hyper-V Linux VM, so far), where host means a server or a VM.</span></span>

<span data-ttu-id="9b66e-111">Разработчики могут использовать среды разработки на базе Windows, Linux или macOS.</span><span class="sxs-lookup"><span data-stu-id="9b66e-111">Developers can use development environments on Windows, Linux, or macOS.</span></span> <span data-ttu-id="9b66e-112">На компьютере разработчика выполняется узел Docker, где развернуты образы Docker с создаваемым приложением и всеми его зависимостями.</span><span class="sxs-lookup"><span data-stu-id="9b66e-112">On the development computer, the developer runs a Docker host where Docker images are deployed, including the app and its dependencies.</span></span> <span data-ttu-id="9b66e-113">Разработчики, использующие Linux или Mac, могут применять узел Docker на базе Linux и создавать образы только для контейнеров Linux.</span><span class="sxs-lookup"><span data-stu-id="9b66e-113">Developers who work on Linux or on the Mac use a Docker host that is Linux based, and they can create images only for Linux containers.</span></span> <span data-ttu-id="9b66e-114">(На компьютерах Mac разработчики могут изменять код приложения и запускать в macOS интерфейс командной строки Docker, но на момент написания данной статьи не могут запускать контейнеры непосредственно в macOS.) В Windows разработчики могут создавать образы для контейнеров Linux или Windows.</span><span class="sxs-lookup"><span data-stu-id="9b66e-114">(Developers working on the Mac can edit code or run the Docker CLI from macOS, but as of the time of this writing, containers don't run directly on macOS.) Developers who work on Windows can create images for either Linux or Windows Containers.</span></span>

<span data-ttu-id="9b66e-115">Docker предоставляет версию [Docker Community Edition (CE)](https://www.docker.com/community-edition) для Windows или macOS, которая позволяет размещать контейнеры в среде разработки и предоставляет дополнительные средства разработки.</span><span class="sxs-lookup"><span data-stu-id="9b66e-115">To host containers in development environments and provide additional developer tools, Docker ships [Docker Community Edition (CE)](https://www.docker.com/community-edition) for Windows or for macOS.</span></span> <span data-ttu-id="9b66e-116">Оба продукта устанавливают необходимую виртуальную машину (узел Docker) для размещения контейнеров.</span><span class="sxs-lookup"><span data-stu-id="9b66e-116">These products install the necessary VM (the Docker host) to host the containers.</span></span> <span data-ttu-id="9b66e-117">Docker также предлагает версию [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition), которая предназначена для корпоративных разработчиков и ИТ-отделов, которые создают, распространяют и выполняют крупные и критически важные приложения в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9b66e-117">Docker also makes available [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition), which is designed for enterprise development and is used by IT teams who build, ship, and run large business-critical applications in production.</span></span>

<span data-ttu-id="9b66e-118">Для выполнения [контейнеров Windows](/virtualization/windowscontainers/about/) есть среды выполнения двух типов:</span><span class="sxs-lookup"><span data-stu-id="9b66e-118">To run [Windows Containers](/virtualization/windowscontainers/about/), there are two types of runtimes:</span></span>

- <span data-ttu-id="9b66e-119">Контейнеры Windows Server изолируют приложение с помощью технологии изоляции процесса и пространства имен.</span><span class="sxs-lookup"><span data-stu-id="9b66e-119">Windows Server Containers provide application isolation through process and namespace isolation technology.</span></span> <span data-ttu-id="9b66e-120">Контейнер Windows Server использует ядро совместно с узлом контейнеров и всеми остальными контейнерами на узле.</span><span class="sxs-lookup"><span data-stu-id="9b66e-120">A Windows Server Container shares a kernel with the container host and with all containers running on the host.</span></span>

- <span data-ttu-id="9b66e-121">Контейнеры Hyper-V увеличивают изоляцию, обеспеченную контейнерами Windows Server, запуская каждый контейнер в оптимизированной виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="9b66e-121">Hyper-V Containers expand on the isolation provided by Windows Server Containers by running each container in a highly optimized virtual machine.</span></span> <span data-ttu-id="9b66e-122">В этой конфигурации ядро узла контейнера не используется совместно с контейнерами Hyper-V, что улучшает изоляцию.</span><span class="sxs-lookup"><span data-stu-id="9b66e-122">In this configuration, the kernel of the container host isn't shared with the Hyper-V Containers, providing better isolation.</span></span>

<span data-ttu-id="9b66e-123">Образы для этих контейнеров создаются и работают одинаково.</span><span class="sxs-lookup"><span data-stu-id="9b66e-123">The images for these containers are created the same way and function the same.</span></span> <span data-ttu-id="9b66e-124">Различие заключается лишь в том, что для создания контейнера из образа с контейнером Hyper-V нужен дополнительный параметр.</span><span class="sxs-lookup"><span data-stu-id="9b66e-124">The difference is in how the container is created from the image running a Hyper-V Container requires an extra parameter.</span></span> <span data-ttu-id="9b66e-125">Дополнительные сведения см. в разделе [Контейнеры Hyper-V](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/hyperv-container).</span><span class="sxs-lookup"><span data-stu-id="9b66e-125">For details, see [Hyper-V Containers](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/hyperv-container).</span></span>

## <a name="comparing-docker-containers-with-virtual-machines"></a><span data-ttu-id="9b66e-126">Сравнение контейнеров Docker с виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="9b66e-126">Comparing Docker containers with virtual machines</span></span>

<span data-ttu-id="9b66e-127">На рисунке 2-3 показано сравнение между виртуальными машинами и контейнерами Docker.</span><span class="sxs-lookup"><span data-stu-id="9b66e-127">Figure 2-3 shows a comparison between VMs and Docker containers.</span></span>

| <span data-ttu-id="9b66e-128">Виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="9b66e-128">Virtual Machines</span></span> | <span data-ttu-id="9b66e-129">Контейнеры Docker</span><span class="sxs-lookup"><span data-stu-id="9b66e-129">Docker Containers</span></span> |
| -----------------| ------------------|
|![Для виртуальных машин на сервере узла создается три базовых уровня: самый нижний инфраструктурный слой; затем операционная система узла и низкоуровневая оболочка; и поверх этого каждая виртуальная машина использует собственную ОС и все необходимые библиотеки.](./media/image3.png)|![Для Docker сервер узла предоставляет только инфраструктуру и операционную систему, а также ядро контейнеров, которое изолирует контейнер с использованием базовых служб операционной системы.](./media/image4.png)|
|<span data-ttu-id="9b66e-132">Виртуальные машины содержат приложение, необходимые библиотеки или двоичные файлы и всю операционную систему.</span><span class="sxs-lookup"><span data-stu-id="9b66e-132">Virtual machines include the application, the required libraries or binaries, and a full guest operating system.</span></span> <span data-ttu-id="9b66e-133">Полная виртуализация требует больше ресурсов, чем создание контейнеров.</span><span class="sxs-lookup"><span data-stu-id="9b66e-133">Full virtualization requires more resources than containerization.</span></span> | <span data-ttu-id="9b66e-134">Контейнеры включают в себя приложение и все его зависимости.</span><span class="sxs-lookup"><span data-stu-id="9b66e-134">Containers include the application and all its dependencies.</span></span> <span data-ttu-id="9b66e-135">Но они используют ядро ОС совместно с другими контейнерами, которые выполняются в изолированных процессах в пользовательском пространстве операционной системы узла.</span><span class="sxs-lookup"><span data-stu-id="9b66e-135">However, they share the OS kernel with other containers, running as isolated processes in user space on the host operating system.</span></span> <span data-ttu-id="9b66e-136">(Это не относится к контейнерам Hyper-V, где каждый контейнер запускается на отдельной виртуальной машине.)</span><span class="sxs-lookup"><span data-stu-id="9b66e-136">(Except in Hyper-V containers, where each container runs inside of a special virtual machine per container.)</span></span> |

<span data-ttu-id="9b66e-137">**Рис. 2-3**.</span><span class="sxs-lookup"><span data-stu-id="9b66e-137">**Figure 2-3**.</span></span> <span data-ttu-id="9b66e-138">Сравнение традиционных виртуальных машин с контейнерами Docker</span><span class="sxs-lookup"><span data-stu-id="9b66e-138">Comparison of traditional virtual machines to Docker containers</span></span>

<span data-ttu-id="9b66e-139">Так как контейнеры требуют гораздо меньше ресурсов (например, им не нужна полная ОС), их проще развертывать и они быстрее запускаются.</span><span class="sxs-lookup"><span data-stu-id="9b66e-139">Because containers require far fewer resources (for example, they don't need a full OS), they're easy to deploy and they start fast.</span></span> <span data-ttu-id="9b66e-140">Это позволяет повысить плотность развертываний, то есть запустить на одной единице оборудования больше служб и сократить затраты на них.</span><span class="sxs-lookup"><span data-stu-id="9b66e-140">This allows you to have higher density, meaning that it allows you to run more services on the same hardware unit, thereby reducing costs.</span></span>

<span data-ttu-id="9b66e-141">Запуск на одном ядре приводит к тому, что уровень изоляции будет ниже, чем на виртуальных машинах.</span><span class="sxs-lookup"><span data-stu-id="9b66e-141">As a side effect of running on the same kernel, you get less isolation than VMs.</span></span>

<span data-ttu-id="9b66e-142">Основная цель образа — привести среду (зависимости) к единообразию в различных развертываниях.</span><span class="sxs-lookup"><span data-stu-id="9b66e-142">The main goal of an image is that it makes the environment (dependencies) the same across different deployments.</span></span> <span data-ttu-id="9b66e-143">Это означает, что вы можете отладить образ на одном компьютере, а затем развернуть его на другом компьютере и получить ту же среду.</span><span class="sxs-lookup"><span data-stu-id="9b66e-143">This means that you can debug it on your machine and then deploy it to another machine with the same environment guaranteed.</span></span>

<span data-ttu-id="9b66e-144">Образ контейнера — это способ упаковки приложения или службы для надежного и воспроизводимого развертывания.</span><span class="sxs-lookup"><span data-stu-id="9b66e-144">A container image is a way to package an app or service and deploy it in a reliable and reproducible way.</span></span> <span data-ttu-id="9b66e-145">Можно сказать, что Docker является не только технологией, но еще философией и процессом.</span><span class="sxs-lookup"><span data-stu-id="9b66e-145">You could say that Docker isn't only a technology but also a philosophy and a process.</span></span>

<span data-ttu-id="9b66e-146">При работе с Docker разработчики никогда не жалуются, что приложение работает только на локальном компьютере, но не в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="9b66e-146">When using Docker, you won't hear developers say, "It works on my machine, why not in production?"</span></span> <span data-ttu-id="9b66e-147">Им достаточно сказать "Выполняется в Docker", так как упакованное приложение Docker будет выполняться в любой поддерживаемой среде Docker. Оно будет работать одинаково во всех сценариях развертывания (разработка, контроль качества, промежуточное размещение и рабочая среда).</span><span class="sxs-lookup"><span data-stu-id="9b66e-147">They can simply say, "It runs on Docker", because the packaged Docker application can be executed on any supported Docker environment, and it runs the way it was intended to on all deployment targets (such as Dev, QA, staging, and production).</span></span>

## <a name="a-simple-analogy"></a><span data-ttu-id="9b66e-148">Простая аналогия</span><span class="sxs-lookup"><span data-stu-id="9b66e-148">A simple analogy</span></span>

<span data-ttu-id="9b66e-149">Возможно, небольшая аналогия поможет вам быстрее освоить ключевую концепцию Docker.</span><span class="sxs-lookup"><span data-stu-id="9b66e-149">Perhaps a simple analogy can help getting the grasp of the core concept of Docker.</span></span>

<span data-ttu-id="9b66e-150">Вернемся ненадолго назад во времени, в 1950-е годы.</span><span class="sxs-lookup"><span data-stu-id="9b66e-150">Let's go back in time to the 1950s for a moment.</span></span> <span data-ttu-id="9b66e-151">Тогда еще не было текстовых редакторов, и повсеместно использовались фотокопировальные устройства (то есть то, что тогда так называлось).</span><span class="sxs-lookup"><span data-stu-id="9b66e-151">There were no word processors, and the photocopiers were used everywhere (kind of).</span></span>

<span data-ttu-id="9b66e-152">Представьте, что вам понадобилось быстро подготовить наборы писем, чтобы отправить их с обычной бумажной почтой в настоящих конвертах с марками и доставить по домашнему адресу клиента (не забывайте, еще не существует электронной почты).</span><span class="sxs-lookup"><span data-stu-id="9b66e-152">Imagine you're responsible for quickly issuing batches of letters as required, to mail them to customers, using real paper and envelopes, to be delivered physically to each customer's address (there was no email back then).</span></span>

<span data-ttu-id="9b66e-153">В какой-то момент вы понимаете, что каждое письмо составлено из широкого набора абзацев, которые выбираются и упорядочиваются по мере необходимости с учетом назначения письма. Вы создаете систему, которая быстро создает нужные письма, и обоснованно надеетесь на существенную прибавку.</span><span class="sxs-lookup"><span data-stu-id="9b66e-153">At some point, you realize the letters are just a composition of a large set of paragraphs, which are picked and arranged as needed, according to the purpose of the letter, so you devise a system to issue letters quickly, expecting to get a hefty raise.</span></span>

<span data-ttu-id="9b66e-154">Вы создали простую систему со следующим алгоритмом:</span><span class="sxs-lookup"><span data-stu-id="9b66e-154">The system is simple:</span></span>

1. <span data-ttu-id="9b66e-155">У вас есть пачка прозрачных листов, каждый из которых содержит один абзац.</span><span class="sxs-lookup"><span data-stu-id="9b66e-155">You begin with a deck of transparent sheets containing one paragraph each.</span></span>

2. <span data-ttu-id="9b66e-156">Чтобы подготовить комплект писем, вы отбираете листы с нужными абзацами, собираете их в стопку и выравниваете так, чтобы все правильно читалось.</span><span class="sxs-lookup"><span data-stu-id="9b66e-156">To issue a set of letters, you pick the sheets with the paragraphs you need, then you stack and align them so they look and read fine.</span></span>

3. <span data-ttu-id="9b66e-157">Теперь вы помещаете готовый набор в фотокопировальное устройство и нажмите кнопку запуска, чтобы изготовить нужное количество копий.</span><span class="sxs-lookup"><span data-stu-id="9b66e-157">Finally, you place the set in the photocopier and press start to produce as many letters as required.</span></span>

<span data-ttu-id="9b66e-158">Это и есть основная концепция Docker в упрощенной форме.</span><span class="sxs-lookup"><span data-stu-id="9b66e-158">So, simplifying, that's the core idea of Docker.</span></span>

<span data-ttu-id="9b66e-159">В Docker каждый слой представляет некоторый набор изменений, которые применяются к файловой системе после выполнения команды, такой как установка программы.</span><span class="sxs-lookup"><span data-stu-id="9b66e-159">In Docker, each layer is the resulting set of changes that happen to the filesystem after executing a command, such as, installing a program.</span></span>

<span data-ttu-id="9b66e-160">Если вы "посмотрите" на файловую систему после копирования очередного слоя, вы увидите все файлы в том состоянии, которое они приняли после установки программы.</span><span class="sxs-lookup"><span data-stu-id="9b66e-160">So, when you "look" at the filesystem after the layer has been copied, you see all the files, included the layer when the program was installed.</span></span>

<span data-ttu-id="9b66e-161">Такой образ можно рассматривать как дополнительный жесткий диск, доступный только для чтения, который готов к установке на "компьютер" с уже установленной операционной системой.</span><span class="sxs-lookup"><span data-stu-id="9b66e-161">You can think of an image as an auxiliary read-only hard disk ready to be installed in a "computer" where the operating system is already installed.</span></span>

<span data-ttu-id="9b66e-162">Соответственно, роль "компьютера" здесь выполняет контейнер, в который устанавливается жесткий диск этого образа.</span><span class="sxs-lookup"><span data-stu-id="9b66e-162">Similarly, you can think of a container as the "computer" with the image hard disk installed.</span></span> <span data-ttu-id="9b66e-163">Контейнер, как и обычный компьютер, можно включать и отключать.</span><span class="sxs-lookup"><span data-stu-id="9b66e-163">The container, just like a computer, can be powered on or off.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="9b66e-164">[Назад](index.md)
>[Вперед](docker-terminology.md)</span><span class="sxs-lookup"><span data-stu-id="9b66e-164">[Previous](index.md)
[Next](docker-terminology.md)</span></span>