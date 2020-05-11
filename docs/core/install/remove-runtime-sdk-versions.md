---
title: Удаление среды выполнения .NET Core и пакета SDK
description: В этой статье объясняется, как определить установленные в текущее время версии среды выполнения .NET Core и пакета SDK и как затем удалить их в Windows, Mac и Linux.
author: thraka
ms.author: adegeo
ms.date: 04/28/2020
zone_pivot_groups: operating-systems-set-one
ms.openlocfilehash: f1482c243ba22fa81c69ede847a0f6b36a9cb83c
ms.sourcegitcommit: d7666f6e49c57a769612602ea7857b927294ce47
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2020
ms.locfileid: "82595765"
---
# <a name="how-to-remove-the-net-core-runtime-and-sdk"></a><span data-ttu-id="517a6-103">Как удалить среду выполнения .NET Core и пакет SDK</span><span class="sxs-lookup"><span data-stu-id="517a6-103">How to remove the .NET Core Runtime and SDK</span></span>

<span data-ttu-id="517a6-104">По мере установки обновленных версий среды выполнения и пакета SDK .NET Core может потребоваться удалить устаревшие версии .NET Core с вашего компьютера.</span><span class="sxs-lookup"><span data-stu-id="517a6-104">Over time, as you install updated versions of the .NET Core runtime and SDK, you may want to remove outdated versions of .NET Core from your machine.</span></span> <span data-ttu-id="517a6-105">При удалении более ранних версий среды выполнения может измениться среда выполнения, выбранная для запуска приложений общей платформы, как описано в статье [Выбор версии .NET Core](../versions/selection.md).</span><span class="sxs-lookup"><span data-stu-id="517a6-105">Removing older versions of the runtime may change the runtime chosen to run shared framework applications, as detailed in the article on [.NET Core version selection](../versions/selection.md).</span></span>

## <a name="should-i-remove-a-version"></a><span data-ttu-id="517a6-106">Нужно ли удалять версию</span><span class="sxs-lookup"><span data-stu-id="517a6-106">Should I remove a version?</span></span>

<span data-ttu-id="517a6-107">[Выбор версии .NET Core](../versions/selection.md) и совместимость среды выполнения .NET Core для различных обновлений обеспечивает безопасное удаление предыдущих версий.</span><span class="sxs-lookup"><span data-stu-id="517a6-107">The [.NET Core version selection](../versions/selection.md) behaviors and the runtime compatibility of .NET Core across updates enables safe removal of previous versions.</span></span> <span data-ttu-id="517a6-108">Обновления среды выполнения .NET Core совместимы в пределах основной версии, например 1.x или 2.x.</span><span class="sxs-lookup"><span data-stu-id="517a6-108">.NET Core runtime updates are compatible within a major version 'band' such as 1.x and 2.x.</span></span> <span data-ttu-id="517a6-109">Кроме того, более поздние выпуски пакета SDK для .NET Core обычно позволяют создавать приложения, совместимые с предыдущими версиями среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="517a6-109">Additionally, newer releases of the .NET Core SDK generally maintain the ability to build applications that target previous versions of the runtime in a compatible manner.</span></span>

<span data-ttu-id="517a6-110">Как правило, требуется только последняя версия пакета SDK и последняя версия исправлений для сред выполнения, необходимых для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="517a6-110">In general, you only need the latest SDK and latest patch version of the runtimes required for your application.</span></span> <span data-ttu-id="517a6-111">Вы можете хранить старые пакеты SDK или версии среды выполнения, например для поддержки приложений на базе *project.json*.</span><span class="sxs-lookup"><span data-stu-id="517a6-111">Instances where you might want to keep older SDK or runtime versions include maintaining *project.json*-based applications.</span></span> <span data-ttu-id="517a6-112">Если у приложения нет конкретных причин, по которым оно должно использовать ранние версии пакета SDK или среды выполнения, вы можете безопасно удалить старые версии.</span><span class="sxs-lookup"><span data-stu-id="517a6-112">Unless your application has specific reasons for earlier SDKs or runtimes, you may safely remove older versions.</span></span>

## <a name="determine-what-is-installed"></a><span data-ttu-id="517a6-113">Определите компоненты, которые нужно установить</span><span class="sxs-lookup"><span data-stu-id="517a6-113">Determine what is installed</span></span>

<span data-ttu-id="517a6-114">Начиная с .NET Core 2.1 можно определить версии пакета SDK и среды выполнения, установленных на вашем компьютере, с помощью команд в .NET CLI.</span><span class="sxs-lookup"><span data-stu-id="517a6-114">Starting with .NET Core 2.1, the .NET CLI has options you can use to list the versions of the SDK and runtime that are installed on your machine.</span></span>  <span data-ttu-id="517a6-115">Чтобы просмотреть список пакетов SDK, установленных на вашем компьютере, выполните команду [`dotnet --list-sdks`](../tools/dotnet.md#options).</span><span class="sxs-lookup"><span data-stu-id="517a6-115">Use [`dotnet --list-sdks`](../tools/dotnet.md#options) to see the list of SDKs installed on your machine.</span></span> <span data-ttu-id="517a6-116">Чтобы просмотреть список сред выполнения, установленных на вашем компьютере, выполните команду [`dotnet --list-runtimes`](../tools/dotnet.md#options).</span><span class="sxs-lookup"><span data-stu-id="517a6-116">Use [`dotnet --list-runtimes`](../tools/dotnet.md#options) to see the list of runtimes installed on your machine.</span></span> <span data-ttu-id="517a6-117">Дополнительные сведения см. в статье [Проверка того, установлена ли платформа .NET Core](how-to-detect-installed-versions.md).</span><span class="sxs-lookup"><span data-stu-id="517a6-117">For more information, see [How to check that .NET Core is already installed](how-to-detect-installed-versions.md).</span></span>

## <a name="uninstall-net-core"></a><span data-ttu-id="517a6-118">Удаление .NET Core</span><span class="sxs-lookup"><span data-stu-id="517a6-118">Uninstall .NET Core</span></span>

::: zone pivot="os-windows"

<span data-ttu-id="517a6-119">Для удаления версий среды выполнения и пакета SDK .NET Core используется диалоговое окно **Программы и компоненты** Windows.</span><span class="sxs-lookup"><span data-stu-id="517a6-119">.NET Core uses the Windows **Apps & features** dialog to remove versions of the .NET Core runtime and SDK.</span></span> <span data-ttu-id="517a6-120">На рисунке ниже показано диалоговое окно **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="517a6-120">The following figure shows the **Apps & features** dialog.</span></span> <span data-ttu-id="517a6-121">Вы можете выполнить поиск по запросу **core sdk** для фильтрации и отображения установленных версий .NET Core.</span><span class="sxs-lookup"><span data-stu-id="517a6-121">You can search for **core sdk** to filter and show installed versions of .NET Core.</span></span>

![Диалоговое окно "Установка и удаление программ" для удаления .NET Core](./media/remove-runtime-sdk-versions/programs-and-features.png)

<span data-ttu-id="517a6-123">Выберите все версии, которые необходимо удалить, и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="517a6-123">Select any versions you want to remove from your machine and click **Uninstall**.</span></span>

::: zone-end

::: zone pivot="os-linux"

<span data-ttu-id="517a6-124">В Linux есть несколько вариантов удаления .NET Core (пакета SDK или среды выполнения).</span><span class="sxs-lookup"><span data-stu-id="517a6-124">There are more options to uninstall .NET Core (either SDK or runtime) on Linux.</span></span> <span data-ttu-id="517a6-125">Лучший способ удаления .NET Core — выполнить действие, противоположное тому, которое использовалось при установке .NET Core.</span><span class="sxs-lookup"><span data-stu-id="517a6-125">The best way for you to uninstall .NET Core is to mirror the action you used to install .NET Core.</span></span> <span data-ttu-id="517a6-126">Конкретные действия зависят от выбранного дистрибутива и метода установки.</span><span class="sxs-lookup"><span data-stu-id="517a6-126">The specifics depend on your chosen distribution and the installation method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="517a6-127">Сведения об установке и удалении .NET Core для систем Red Hat см. в [Руководстве по началу работы с Red Hat](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel).</span><span class="sxs-lookup"><span data-stu-id="517a6-127">For Red Hat installations, consult the [Red Hat Getting Started Guide](https://access.redhat.com/documentation/en-us/net_core/2.0/html/getting_started_guide/gs_install_dotnet#install_register_rehel) for information on installing and uninstalling .NET Core.</span></span>

<span data-ttu-id="517a6-128">Начиная с .NET Core 2.1 нет необходимости удалять пакет SDK для .NET Core при его обновлении с помощью диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="517a6-128">Starting with .NET Core 2.1, there's no need to uninstall the .NET Core SDK when upgrading it using a package manager.</span></span> <span data-ttu-id="517a6-129">Диспетчер пакетов `update` или команды `refresh` автоматически удалят старую версию после успешной установки более новой версии.</span><span class="sxs-lookup"><span data-stu-id="517a6-129">The package manager `update` or `refresh` commands will automatically remove the older version upon the successful installation of a newer version.</span></span>

<span data-ttu-id="517a6-130">Если вы установили .NET Core с помощью диспетчера пакетов, для удаления пакета SDK для .NET или среды выполнения используется тот же диспетчер пакетов.</span><span class="sxs-lookup"><span data-stu-id="517a6-130">If you installed .NET Core using a package manager, you use that same package manager to uninstall .NET SDK or runtime.</span></span> <span data-ttu-id="517a6-131">.NET Core поддерживает большинство популярных менеджеров пакетов.</span><span class="sxs-lookup"><span data-stu-id="517a6-131">.NET Core installations support most popular package managers.</span></span> <span data-ttu-id="517a6-132">Точный синтаксис команды для вашей среды см. в документации по вашему дистрибутиву:</span><span class="sxs-lookup"><span data-stu-id="517a6-132">Consult the documentation for your distribution's package manager for the precise syntax in your environment:</span></span>

- <span data-ttu-id="517a6-133">[apt-get(8)](https://linux.die.net/man/8/apt-get) используется в системах на основе Debian, включая Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="517a6-133">[apt-get(8)](https://linux.die.net/man/8/apt-get) is used by Debian based systems, including Ubuntu.</span></span>
- <span data-ttu-id="517a6-134">[yum(8)](https://linux.die.net/man/8/yum) используется в Fedora, CentOS и Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="517a6-134">[yum(8)](https://linux.die.net/man/8/yum) is used on Fedora, CentOS, and Oracle Linux.</span></span>
- <span data-ttu-id="517a6-135">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) используется в openSUSE и SUSE Linux Enterprise System (SLES).</span><span class="sxs-lookup"><span data-stu-id="517a6-135">[zypper(8)](https://en.opensuse.org/SDB:Zypper_manual_(plain)) is used on openSUSE and SUSE Linux Enterprise System (SLES).</span></span>
- <span data-ttu-id="517a6-136">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) используется в Fedora.</span><span class="sxs-lookup"><span data-stu-id="517a6-136">[dnf(8)](https://dnf.readthedocs.io/en/latest/command_ref.html) is used on Fedora.</span></span>

<span data-ttu-id="517a6-137">Практически во всех случаях для удаления пакета используется команда `remove`.</span><span class="sxs-lookup"><span data-stu-id="517a6-137">In almost all cases, the command to remove a package is `remove`.</span></span>

<span data-ttu-id="517a6-138">Для установки пакета SDK для .NET Core в большинстве диспетчеров пакетов используется имя пакета `dotnet-sdk`, за которым следует номер версии.</span><span class="sxs-lookup"><span data-stu-id="517a6-138">The package name for the .NET Core SDK installation for most package managers is `dotnet-sdk`, followed by the version number.</span></span> <span data-ttu-id="517a6-139">Начиная с версии 2.1.300 пакета SDK для .NET Core и версии `2.1` среды выполнения необходимы только основной номер версии и дополнительный номер версии: например, для версии 2.1.300 пакета SDK для .NET Core можно указать пакет `dotnet-sdk-2.1`.</span><span class="sxs-lookup"><span data-stu-id="517a6-139">Starting with the version 2.1.300 of the .NET Core SDK and version `2.1` of the runtime, only the major and minor version numbers are necessary: for example, the .NET Core SDK version 2.1.300 can be referenced as the package `dotnet-sdk-2.1`.</span></span> <span data-ttu-id="517a6-140">В предыдущих версиях необходимо указать полную строку версии, например, для версии 2.1.200 пакета SDK для .NET Core потребовалось бы указать `dotnet-sdk-2.1.200`.</span><span class="sxs-lookup"><span data-stu-id="517a6-140">Prior versions require the entire version string: for example, `dotnet-sdk-2.1.200` would be required for version 2.1.200 of the .NET Core SDK.</span></span>

<span data-ttu-id="517a6-141">Для компьютеров, на которых установлена только среда выполнения без пакета SDK, используется имя пакета `dotnet-runtime-<version>` для среды выполнения .NET Core и `aspnetcore-runtime-<version>` для стека всей среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="517a6-141">For machines that have installed only the runtime, and not the SDK, the package name is `dotnet-runtime-<version>` for the .NET Core runtime, and `aspnetcore-runtime-<version>` for the entire runtime stack.</span></span>

<span data-ttu-id="517a6-142">Для .NET Core версий ниже 2.0 ведущее приложение не удалялось при удалении пакета SDK с помощью диспетчера пакетов.</span><span class="sxs-lookup"><span data-stu-id="517a6-142">.NET Core installations earlier than 2.0 didn't uninstall the host application when the SDK was uninstalled using the package manager.</span></span> <span data-ttu-id="517a6-143">При использовании `apt-get` применяется следующая команда:</span><span class="sxs-lookup"><span data-stu-id="517a6-143">Using `apt-get`, the command is:</span></span>

```bash
apt-get remove dotnet-host
```

<span data-ttu-id="517a6-144">Обратите внимание, что с `dotnet-host`не связана версия.</span><span class="sxs-lookup"><span data-stu-id="517a6-144">Note that there's no version attached to `dotnet-host`.</span></span>

<span data-ttu-id="517a6-145">Если вы установили .NET Core из tar-архива, необходимо выполнить удаление вручную.</span><span class="sxs-lookup"><span data-stu-id="517a6-145">If you installed using a tarball, you must remove .NET Core using the manual method.</span></span>

<span data-ttu-id="517a6-146">На компьютерах Linux необходимо отдельно удалить пакеты SDK и среды выполнения, удаляя каталоги с версиями.</span><span class="sxs-lookup"><span data-stu-id="517a6-146">On Linux, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="517a6-147">При их удалении пакет SDK и среда выполнения также удаляются с диска.</span><span class="sxs-lookup"><span data-stu-id="517a6-147">Removing them deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="517a6-148">Например, чтобы удалить пакет SDK и среду выполнения версии 1.0.1, можно использовать следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="517a6-148">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="517a6-149">Родительские каталоги для пакета SDK и среды выполнения указаны в выходных данных команд `dotnet --list-sdks` и `dotnet --list-runtimes`, как показано в приведенной выше таблице.</span><span class="sxs-lookup"><span data-stu-id="517a6-149">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

::: zone-end

::: zone pivot="os-macos"

<span data-ttu-id="517a6-150">На компьютерах Mac необходимо отдельно удалить пакеты SDK и среды выполнения, удаляя каталоги с версиями.</span><span class="sxs-lookup"><span data-stu-id="517a6-150">On Mac, you must remove the SDKs and runtimes separately, by removing the versioned directories.</span></span> <span data-ttu-id="517a6-151">При их удалении пакет SDK и среда выполнения также удаляются с диска.</span><span class="sxs-lookup"><span data-stu-id="517a6-151">Removing them deletes the SDK and runtime from disk.</span></span> <span data-ttu-id="517a6-152">Например, чтобы удалить пакет SDK и среду выполнения версии 1.0.1, можно использовать следующие команды Bash:</span><span class="sxs-lookup"><span data-stu-id="517a6-152">For example, to remove the 1.0.1 SDK and runtime, you would use the following bash commands:</span></span>

```bash
version="1.0.1"
sudo rm -rf /usr/local/share/dotnet/sdk/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.NETCore.App/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.All/$version
sudo rm -rf /usr/local/share/dotnet/shared/Microsoft.AspNetCore.App/$version
sudo rm -rf /usr/local/share/dotnet/host/fxr/$version
```

<span data-ttu-id="517a6-153">Родительские каталоги для пакета SDK и среды выполнения указаны в выходных данных команд `dotnet --list-sdks` и `dotnet --list-runtimes`, как показано в приведенной выше таблице.</span><span class="sxs-lookup"><span data-stu-id="517a6-153">The parent directories for the SDK and runtime are listed in the output from the `dotnet --list-sdks` and `dotnet --list-runtimes` command, as shown in the earlier table.</span></span>

::: zone-end

## <a name="net-core-uninstall-tool"></a><span data-ttu-id="517a6-154">Средство удаления .NET Core</span><span class="sxs-lookup"><span data-stu-id="517a6-154">.NET Core Uninstall Tool</span></span>

<span data-ttu-id="517a6-155">[Средство удаления .NET Core](../additional-tools/uninstall-tool.md) (`dotnet-core-uninstall`) позволяет удалять пакеты SDK и среды выполнения .NET Core из системы.</span><span class="sxs-lookup"><span data-stu-id="517a6-155">The [.NET Core Uninstall Tool](../additional-tools/uninstall-tool.md) (`dotnet-core-uninstall`) lets you remove .NET Core SDKs and runtimes from a system.</span></span> <span data-ttu-id="517a6-156">Указать удаляемые версии можно с помощью ряда параметров.</span><span class="sxs-lookup"><span data-stu-id="517a6-156">A collection of options is available to specify which versions should be uninstalled.</span></span>

## <a name="visual-studio-dependency-on-net-core-sdk-versions"></a><span data-ttu-id="517a6-157">Зависимость Visual Studio от версий пакетов SDK для .NET Core</span><span class="sxs-lookup"><span data-stu-id="517a6-157">Visual Studio dependency on .NET Core SDK versions</span></span>

<span data-ttu-id="517a6-158">До появления Visual Studio 2019 версии 16.3, установщики Visual Studio пользовались автономным установщиком пакета SDK для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="517a6-158">Before Visual Studio 2019 version 16.3, Visual Studio installers called the standalone .NET Core SDK installer.</span></span> <span data-ttu-id="517a6-159">В результате версии пакета SDK отображаются в диалоговом окне Windows **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="517a6-159">As a result, the SDK versions appear in the Windows **Apps & features** dialog.</span></span> <span data-ttu-id="517a6-160">Удаление пакетов SDK для .NET Core, установленных Visual Studio с помощью автономного установщика, может нарушить работу Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="517a6-160">Removing .NET Core SDKs that were installed by Visual Studio using the standalone installer may break Visual Studio.</span></span> <span data-ttu-id="517a6-161">Если после удаления пакетов SDK в Visual Studio возникают проблемы, запустите "Восстановление" для этой конкретной версии Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="517a6-161">If Visual Studio has problems after you uninstall SDKs, run Repair on that specific version of Visual Studio.</span></span> <span data-ttu-id="517a6-162">В следующей таблице показаны некоторые зависимости Visual Studio от пакета SDK для версий .NET Core.</span><span class="sxs-lookup"><span data-stu-id="517a6-162">The following table shows some of the Visual Studio dependencies on .NET Core SDK versions:</span></span>

| <span data-ttu-id="517a6-163">Версия Visual Studio</span><span class="sxs-lookup"><span data-stu-id="517a6-163">Visual Studio version</span></span>           | <span data-ttu-id="517a6-164">Версия пакета SDK для .NET Core</span><span class="sxs-lookup"><span data-stu-id="517a6-164">.NET Core SDK version</span></span>          |
|---------------------------------|--------------------------------|
| <span data-ttu-id="517a6-165">Visual Studio 2019 версии 16.2</span><span class="sxs-lookup"><span data-stu-id="517a6-165">Visual Studio 2019 version 16.2</span></span> | <span data-ttu-id="517a6-166">пакет SDK для NET Core 2.2.4xx, 2.1.8xx</span><span class="sxs-lookup"><span data-stu-id="517a6-166">.NET Core SDK 2.2.4xx, 2.1.8xx</span></span> |
| <span data-ttu-id="517a6-167">Visual Studio 2019 версии 16.1</span><span class="sxs-lookup"><span data-stu-id="517a6-167">Visual Studio 2019 version 16.1</span></span> | <span data-ttu-id="517a6-168">пакет SDK для .NET Core 2.2.3xx, 2.1.7xx</span><span class="sxs-lookup"><span data-stu-id="517a6-168">.NET Core SDK 2.2.3xx, 2.1.7xx</span></span> |
| <span data-ttu-id="517a6-169">Visual Studio 2019 версии 16.0</span><span class="sxs-lookup"><span data-stu-id="517a6-169">Visual Studio 2019 version 16.0</span></span> | <span data-ttu-id="517a6-170">пакет SDK для .NET Core 2.2.2xx, 2.1.6xx</span><span class="sxs-lookup"><span data-stu-id="517a6-170">.NET Core SDK 2.2.2xx, 2.1.6xx</span></span> |
| <span data-ttu-id="517a6-171">Visual Studio 2017 версии 15.9</span><span class="sxs-lookup"><span data-stu-id="517a6-171">Visual Studio 2017 version 15.9</span></span> | <span data-ttu-id="517a6-172">Пакет SDK для .NET Core 2.2.1xx, 2.1.5xx</span><span class="sxs-lookup"><span data-stu-id="517a6-172">.NET Core SDK 2.2.1xx, 2.1.5xx</span></span> |
| <span data-ttu-id="517a6-173">Visual Studio 2017 версии 15.8</span><span class="sxs-lookup"><span data-stu-id="517a6-173">Visual Studio 2017 version 15.8</span></span> | <span data-ttu-id="517a6-174">Пакет SDK для .NET Core 2.1.4xx</span><span class="sxs-lookup"><span data-stu-id="517a6-174">.NET Core SDK 2.1.4xx</span></span>          |

<span data-ttu-id="517a6-175">Visual Studio 2019 версии 16.3 и выше управляет собственной копией пакета SDK для .NET Core.</span><span class="sxs-lookup"><span data-stu-id="517a6-175">Starting with Visual Studio 2019 version 16.3, Visual Studio is in charge of its own copy of the .NET Core SDK.</span></span> <span data-ttu-id="517a6-176">По этой причине вы больше не встретите эти версии пакета SDK в диалоговом окне **Программы и компоненты**.</span><span class="sxs-lookup"><span data-stu-id="517a6-176">For that reason, you no longer see those SDK versions in the **Apps & features** dialog.</span></span>

## <a name="remove-the-nuget-fallback-folder"></a><span data-ttu-id="517a6-177">Удаление резервной папки NuGet</span><span class="sxs-lookup"><span data-stu-id="517a6-177">Remove the NuGet fallback folder</span></span>

<span data-ttu-id="517a6-178">До создания пакета SDK для версии .NET Core 3.0 установщики пакета SDK для .NET Core использовали папку *NuGetFallbackFolder* для хранения кэша пакетов NuGet.</span><span class="sxs-lookup"><span data-stu-id="517a6-178">Before .NET Core 3.0 SDK, the .NET Core SDK installers used a folder named *NuGetFallbackFolder* to store a cache of NuGet packages.</span></span> <span data-ttu-id="517a6-179">Этот кэш использовался во время таких операций, как `dotnet restore` или `dotnet build /t:Restore`.</span><span class="sxs-lookup"><span data-stu-id="517a6-179">This cache was used during operations such as `dotnet restore` or `dotnet build /t:Restore`.</span></span> <span data-ttu-id="517a6-180">*NuGetFallbackFolder* находится в папке *C:\Program Files\dotnet\sdk* в Windows и */usr/local/share/dotnet/sdk* — в macOS.</span><span class="sxs-lookup"><span data-stu-id="517a6-180">The *NuGetFallbackFolder* is located at *C:\Program Files\dotnet\sdk* on Windows and at */usr/local/share/dotnet/sdk* on macOS.</span></span>

<span data-ttu-id="517a6-181">Вы можете удалить эту папку, если:</span><span class="sxs-lookup"><span data-stu-id="517a6-181">You may want to remove this folder, if:</span></span>

- <span data-ttu-id="517a6-182">Разработка выполняется только с использованием пакета SDK для .NET Core 3.0 или более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="517a6-182">You're only developing using .NET Core 3.0 SDK or later versions.</span></span>
- <span data-ttu-id="517a6-183">Разработка выполняется с использованием пакета SDK для .NET Core версий до 3.0, но вы можете работать в режиме "в сети".</span><span class="sxs-lookup"><span data-stu-id="517a6-183">You're developing using .NET Core SDK versions earlier than 3.0, but you can work online.</span></span>

<span data-ttu-id="517a6-184">Если необходимо, вы можете удалить резервную папку NuGet, но для этого вам понадобятся права администратора.</span><span class="sxs-lookup"><span data-stu-id="517a6-184">If you want to remove the NuGet fallback folder, you can delete it, but you'll need admin privileges to do so.</span></span>

<span data-ttu-id="517a6-185">Не рекомендуется удалять папку *dotnet*.</span><span class="sxs-lookup"><span data-stu-id="517a6-185">It's not recommended to delete the *dotnet* folder.</span></span> <span data-ttu-id="517a6-186">Это приведет к удалению всех ранее установленных глобальных средств.</span><span class="sxs-lookup"><span data-stu-id="517a6-186">Doing so would remove any global tools you've previously installed.</span></span> <span data-ttu-id="517a6-187">Также, в Windows:</span><span class="sxs-lookup"><span data-stu-id="517a6-187">Also, on Windows:</span></span>

- <span data-ttu-id="517a6-188">Работа Visual Studio 2019 версии 16.3 и более поздних версий будет нарушена.</span><span class="sxs-lookup"><span data-stu-id="517a6-188">You'll break Visual Studio 2019 version 16.3 and later versions.</span></span> <span data-ttu-id="517a6-189">Для восстановления можно запустить **Восстановление**.</span><span class="sxs-lookup"><span data-stu-id="517a6-189">You can run **Repair** to recover.</span></span>
- <span data-ttu-id="517a6-190">Если в диалоговом окне **Программы и компоненты** есть записи пакета SDK для .NET Core, они будут потеряны.</span><span class="sxs-lookup"><span data-stu-id="517a6-190">If there are .NET Core SDK entries in the **Apps & features** dialog, they'll be orphaned.</span></span>