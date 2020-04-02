---
title: Практическое руководство. Проверка содержимого сборки с помощью MetadataLoadContext
description: Сведения об использовании MetadataLoadContext, API, позволяющее загружать сборки .NET для целей проверки.
author: MSDN-WhiteKnight
ms.date: 03/10/2020
ms.technology: dotnet-standard
ms.openlocfilehash: a782b2db4fb62cfaedaa6768e2131bda6bec864c
ms.sourcegitcommit: b75a45f0cfe012b71b45dd9bf723adf32369d40c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/24/2020
ms.locfileid: "80229275"
---
# <a name="how-to-inspect-assembly-contents-using-metadataloadcontext"></a><span data-ttu-id="2c48b-103">Практическое руководство. Проверка содержимого сборки с помощью MetadataLoadContext</span><span class="sxs-lookup"><span data-stu-id="2c48b-103">How to: Inspect assembly contents using MetadataLoadContext</span></span>

<span data-ttu-id="2c48b-104">API отражения в .NET по умолчанию позволяет разработчикам проверять содержимое сборок, загруженных в основной контекст выполнения.</span><span class="sxs-lookup"><span data-stu-id="2c48b-104">The reflection API in .NET by default enables developers to inspect the contents of assemblies loaded into the main execution context.</span></span> <span data-ttu-id="2c48b-105">Однако иногда невозможно загрузить сборку в контекст выполнения, например, если она была скомпилирована для другой архитектуры платформы или процессора либо если это [базовая сборка](reference-assemblies.md).</span><span class="sxs-lookup"><span data-stu-id="2c48b-105">However, sometimes it isn't possible to load an assembly into the execution context, for example, because it was compiled for another platform or processor architecture, or it's a [reference assembly](reference-assemblies.md).</span></span> <span data-ttu-id="2c48b-106">API <xref:System.Reflection.MetadataLoadContext?displayProperty=fullName> позволяет загружать и проверять такие сборки.</span><span class="sxs-lookup"><span data-stu-id="2c48b-106">The <xref:System.Reflection.MetadataLoadContext?displayProperty=fullName> API allows you to load and inspect such assemblies.</span></span> <span data-ttu-id="2c48b-107">Сборки, загруженные в <xref:System.Reflection.MetadataLoadContext>, обрабатываются только как метаданные, то есть вы можете проверять типы в сборке, но не выполнять код, содержащийся в ней.</span><span class="sxs-lookup"><span data-stu-id="2c48b-107">Assemblies loaded into the <xref:System.Reflection.MetadataLoadContext> are treated only as metadata, that is, you can examine types in the assembly, but you can't execute any code contained in it.</span></span> <span data-ttu-id="2c48b-108">В отличие от основного контекста выполнения <xref:System.Reflection.MetadataLoadContext> не загружает зависимости из текущего каталога автоматически. Вместо этого используется пользовательская логика привязки, предоставляемая <xref:System.Reflection.MetadataAssemblyResolver>, переданной в нее.</span><span class="sxs-lookup"><span data-stu-id="2c48b-108">Unlike the main execution context, the <xref:System.Reflection.MetadataLoadContext> doesn't automatically load dependencies from the current directory; instead it uses the custom binding logic provided by the <xref:System.Reflection.MetadataAssemblyResolver> passed to it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c48b-109">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2c48b-109">Prerequisites</span></span>

<span data-ttu-id="2c48b-110">Чтобы использовать <xref:System.Reflection.MetadataLoadContext>, установите пакет NuGet [System.Reflection.MetadataLoadContext](https://www.nuget.org/packages/System.Reflection.MetadataLoadContext).</span><span class="sxs-lookup"><span data-stu-id="2c48b-110">To use <xref:System.Reflection.MetadataLoadContext>, install the [System.Reflection.MetadataLoadContext](https://www.nuget.org/packages/System.Reflection.MetadataLoadContext) NuGet package.</span></span> <span data-ttu-id="2c48b-111">Она поддерживается в любой целевой платформе, совместимой с .NET Standard 2.0, например .NET Core 2.0 или .NET Framework 4.6.1.</span><span class="sxs-lookup"><span data-stu-id="2c48b-111">It is supported on any .NET Standard 2.0-compliant target framework, for example, .NET Core 2.0 or .NET Framework 4.6.1.</span></span>

## <a name="create-metadataassemblyresolver-for-metadataloadcontext"></a><span data-ttu-id="2c48b-112">Создание MetadataAssemblyResolver для MetadataLoadContext</span><span class="sxs-lookup"><span data-stu-id="2c48b-112">Create MetadataAssemblyResolver for MetadataLoadContext</span></span>

<span data-ttu-id="2c48b-113">Создание <xref:System.Reflection.MetadataLoadContext> требует предоставления экземпляра <xref:System.Reflection.MetadataAssemblyResolver>.</span><span class="sxs-lookup"><span data-stu-id="2c48b-113">Creating the <xref:System.Reflection.MetadataLoadContext> requires providing the instance of the <xref:System.Reflection.MetadataAssemblyResolver>.</span></span> <span data-ttu-id="2c48b-114">Самый простой способ указать, что он использует <xref:System.Reflection.PathAssemblyResolver>, который разрешает сборки из заданной коллекции строк пути сборки.</span><span class="sxs-lookup"><span data-stu-id="2c48b-114">The simplest way to provide one is to use the <xref:System.Reflection.PathAssemblyResolver>, which resolves assemblies from the given collection of assembly path strings.</span></span> <span data-ttu-id="2c48b-115">Эта коллекция, помимо сборок, которые необходимо проверить напрямую, также должна включать все необходимые зависимости.</span><span class="sxs-lookup"><span data-stu-id="2c48b-115">This collection, besides assemblies you want to inspect directly, should also include all needed dependencies.</span></span> <span data-ttu-id="2c48b-116">Например, для чтения настраиваемого атрибута, расположенного во внешней сборке, следует включить эту сборку, иначе будет вызвано исключение.</span><span class="sxs-lookup"><span data-stu-id="2c48b-116">For example, to read the custom attribute located in an external assembly, you should include that assembly or an exception will be thrown.</span></span> <span data-ttu-id="2c48b-117">В большинстве случаев следует включать по крайней мере *основную сборку*, то есть сборку, содержащую встроенные системные типы, такие как <xref:System.Object?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="2c48b-117">In most cases, you should include at least the *core assembly*, that is, the assembly containing built-in system types, such as <xref:System.Object?displayProperty=nameWithType>.</span></span> <span data-ttu-id="2c48b-118">В следующем коде показано, как создать <xref:System.Reflection.PathAssemblyResolver> с помощью коллекции, состоящей из проверенной сборки и основной сборки текущей среды выполнения:</span><span class="sxs-lookup"><span data-stu-id="2c48b-118">The following code shows how to create the <xref:System.Reflection.PathAssemblyResolver> using the collection consisting of the inspected assembly and the current runtime's core assembly:</span></span>

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CoreAssembly)]

<span data-ttu-id="2c48b-119">Если требуется доступ ко всем типам BCL, в коллекцию можно включить все сборки среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="2c48b-119">If you need access to all BCL types, you can include all runtime assemblies in the collection.</span></span> <span data-ttu-id="2c48b-120">В следующем коде показано, как создать <xref:System.Reflection.PathAssemblyResolver> с помощью коллекции, состоящей из проверенной сборки и все сборки текущей среды выполнения:</span><span class="sxs-lookup"><span data-stu-id="2c48b-120">The following code shows how to create the <xref:System.Reflection.PathAssemblyResolver> using the collection consisting of the inspected assembly and all assemblies of the current runtime:</span></span>

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#RuntimeAssemblies)]

## <a name="create-metadataloadcontext"></a><span data-ttu-id="2c48b-121">Создание MetadataLoadContext</span><span class="sxs-lookup"><span data-stu-id="2c48b-121">Create MetadataLoadContext</span></span>

<span data-ttu-id="2c48b-122">Чтобы создать <xref:System.Reflection.MetadataLoadContext>, вызовите его конструктор <xref:System.Reflection.MetadataLoadContext.%23ctor%28System.Reflection.MetadataAssemblyResolver%2CSystem.String%29>, передав ранее созданный <xref:System.Reflection.MetadataAssemblyResolver> в качестве первого параметра и основное имя сборки в качестве второго параметра.</span><span class="sxs-lookup"><span data-stu-id="2c48b-122">To create the <xref:System.Reflection.MetadataLoadContext>, invoke its constructor <xref:System.Reflection.MetadataLoadContext.%23ctor%28System.Reflection.MetadataAssemblyResolver%2CSystem.String%29>, passing the previously created <xref:System.Reflection.MetadataAssemblyResolver> as the first parameter and the core assembly name as the second parameter.</span></span> <span data-ttu-id="2c48b-123">Имя основной сборки можно опустить, в этом случае конструктор попытается использовать имена по умолчанию: "mscorlib", "System.Runtime" или "netstandard".</span><span class="sxs-lookup"><span data-stu-id="2c48b-123">You can omit the core assembly name, in which case the constructor will attempt to use default names: "mscorlib", "System.Runtime", or "netstandard".</span></span>

<span data-ttu-id="2c48b-124">После создания контекста в него можно загрузить сборки с помощью таких методов, как <xref:System.Reflection.MetadataLoadContext.LoadFromAssemblyPath%2A>.</span><span class="sxs-lookup"><span data-stu-id="2c48b-124">After you've created the context, you can load assemblies into it using methods such as <xref:System.Reflection.MetadataLoadContext.LoadFromAssemblyPath%2A>.</span></span> <span data-ttu-id="2c48b-125">Все API отражения можно использовать в загруженных сборках, за исключением тех, которые используют выполнение кода.</span><span class="sxs-lookup"><span data-stu-id="2c48b-125">You can use all reflection APIs on loaded assemblies except ones that involve code execution.</span></span> <span data-ttu-id="2c48b-126">Метод <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A> требует выполнения конструкторов, поэтому, если необходимо исследовать пользовательские атрибуты в <xref:System.Reflection.MetadataLoadContext>, вместо этого следует использовать метод <xref:System.Reflection.MemberInfo.GetCustomAttributesData%2A>.</span><span class="sxs-lookup"><span data-stu-id="2c48b-126">The <xref:System.Reflection.MemberInfo.GetCustomAttributes%2A> method does involve the execution of constructors, so use the <xref:System.Reflection.MemberInfo.GetCustomAttributesData%2A> method instead when you need to examine custom attributes in the <xref:System.Reflection.MetadataLoadContext>.</span></span>

<span data-ttu-id="2c48b-127">Следующий пример кода создает <xref:System.Reflection.MetadataLoadContext>, загружает в него сборку и выводит атрибуты сборки в консоль:</span><span class="sxs-lookup"><span data-stu-id="2c48b-127">The following code sample creates <xref:System.Reflection.MetadataLoadContext>, loads the assembly into it, and outputs assembly attributes into the console:</span></span>

[!code-csharp[](snippets/inspect-contents-using-metadataloadcontext/MetadataLoadContextSnippets.cs#CreateContext)]

## <a name="example"></a><span data-ttu-id="2c48b-128">Пример</span><span class="sxs-lookup"><span data-stu-id="2c48b-128">Example</span></span>

<span data-ttu-id="2c48b-129">Пример полного кода см. [Проверка содержимого сборки с помощью MetadataLoadContext](https://docs.microsoft.com/samples/dotnet/samples/inspect-assembly-contents-using-metadataloadcontext/).</span><span class="sxs-lookup"><span data-stu-id="2c48b-129">For a complete code example, see [Inspect assembly contents using MetadataLoadContext](https://docs.microsoft.com/samples/dotnet/samples/inspect-assembly-contents-using-metadataloadcontext/).</span></span>