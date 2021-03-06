---
title: Управление доступом для кода
description: Узнайте о механизме управления доступом для кода в .NET, который помогает защитить компьютерные системы от вредоносного мобильного кода.
ms.date: 03/30/2017
helpviewer_keywords:
- named permission sets, code access security
- call stacks
- malicious code
- stack walk
- security [.NET Framework], code access security
- permissions [.NET Framework], code access security
- trusted code
- mobile code security
- unmanaged code, code access security
- granting permissions, code access security
- user authentication, code access security
- code access security
ms.assetid: 859af632-c80d-4736-8d6f-1e01b09ce127
ms.openlocfilehash: b5c32afb26c7b4bf7f8585c43ac11e57ebb5d015
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554870"
---
# <a name="code-access-security"></a>Управление доступом для кода

[!INCLUDE[net_security_note](../../../includes/net-security-note-md.md)]  
  
 Современные, в высокой степени взаимосвязанные компьютерные системы часто подвержены воздействию кода из разных, иногда неизвестных источников. Код можно вложить в электронную почту, содержащуюся в документах или скачать через Интернет. К сожалению, многие пользователи уже на собственном опыте испытали действие небезопасного кода, включая вирусы и черви, который может повреждать и уничтожать данные, приводя к потере времени и денег.  
  
 Наиболее распространенные механизмы безопасности предоставляют пользователям права на основе их учетных данных (обычно пароль) и ограничивают ресурсы (часто каталоги и файлы), к которым пользователю разрешен доступ. Однако этот подход неспособен решить некоторые проблемы: пользователи получают код из множества источников, некоторые из которых могут быть ненадежными; код может содержать ошибки или уязвимые места, которые могут использоваться вредоносным кодом. Кроме того, код в некоторых случаях может выполнять действия без ведома пользователя. В результате возможно повреждение компьютерных систем и утечка конфиденциальных данных, когда осмотрительные и благонадежные пользователи запускают вредоносное или содержащее множество ошибок программное обеспечение. Большинство механизмов безопасности операционной системы требует, чтобы каждый фрагмент кода был доверенным для выполнения, за исключением сценариев на веб-странице. Таким образом, необходим механизм безопасности с широкой областью применения, позволяющий коду, полученному от одной компьютерной системы, безопасно выполняться в другой системе даже при отсутствии отношений доверия между этими системами.  
  
 В целях защиты компьютерных систем от вредоносного мобильного кода, обеспечения возможности безопасного исполнения кода, поступившего из неизвестных источников, и защиты доверенного кода от преднамеренного или случайного нарушения безопасности платформа .NET Framework предлагает механизм безопасности, называемый управлением доступом для кода. Управление доступом для кода позволяет определять разные уровни надежности для кода, в зависимости от происхождения и других параметров его удостоверения. Управление доступом для кода также обеспечивает соблюдение различных уровней доверия для кода, минимизируя количество кода, для выполнения которого требуется полное доверие. С помощью управления доступом для кода можно снизить вероятность того, что код будет использован не по назначению вредоносным или содержащим множество ошибок кодом. Оно может также ограничить вашу ответственность, так как вы можете указать для кода набора операций, разрешенных к выполнению. Управление доступом для кода помогает также снизить уровень возможного ущерба от уязвимых мест в коде.  
  
> [!NOTE]
> В .NET Framework 4 были внесены значительные изменения в систему управления доступом для кода. Наиболее заметным изменением является [прозрачность безопасности](security-transparent-code.md), но существуют и другие существенные изменения, влияющие на управление доступом для кода. Сведения об этих изменениях см. в разделе [изменения в системе безопасности](/previous-versions/dotnet/framework/security/security-changes).  
  
 Управление доступом для кода в основном затрагивает код библиотек и приложения с частичным доверием. Разработчики библиотек должны защищать свой код от несанкционированного доступа из приложений с частичным доверием. Приложения с частичным доверием — это приложения, загружаемые из внешних источников, например Интернета. Приложения, установленные на локальном компьютере или в локальной интрасети, выполняются с полным доверием. Безопасность приложений с полным доверием не влияет на управление доступом для кода, если они не помечены как [прозрачные для безопасности](security-transparent-code.md), так как они являются полностью доверенными. Единственное ограничение для приложений с полным доверием состоит в том, что приложения с атрибутом <xref:System.Security.SecurityTransparentAttribute> не могут вызывать код, помеченный атрибутом <xref:System.Security.SecurityCriticalAttribute>. Приложения с частичным доверием должны запускаться в "песочнице" (например, в браузере Internet Explorer), чтобы к ним применялось управление доступом для кода. Если вы загрузили приложение из Интернета и попытаетесь запустить его с рабочего стола, вы получите <xref:System.NotSupportedException> сообщение об ошибке: "предпринята попытка загрузить сборку из сетевого расположения, что привело бы к изолированной сборке в предыдущих версиях .NET Framework. Этот выпуск .NET Framework не включает политику CAS по умолчанию, поэтому данная загрузка может быть опасной". Если вы уверены, что приложение может быть доверенным, можно включить его для запуска с полным доверием с помощью [ \<loadFromRemoteSources> элемента](../configure-apps/file-schema/runtime/loadfromremotesources-element.md). Сведения о запуске приложения в песочнице см. в разделе [как запустить частично доверенный код в песочнице](how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
 Любой управляемый код, предназначенный для среды CLR, получает преимущества управления доступом для кода, даже если он не выполняет ни одного вызова управления доступом для кода. Дополнительные сведения см. в разделе [Code Access Security Basics](code-access-security-basics.md).  
  
<a name="key_functions"></a>
## <a name="key-functions-of-code-access-security"></a>Ключевые функции управления доступом для кода  
 Управление доступом для кода помогает ограничить доступ кода к защищенным ресурсам и операциям. В.NET Framework управление доступом для кода выполняет следующие функции:  
  
- Определяет разрешения и наборы разрешений, представляющих право доступа к различным системным ресурсам.  
  
- Дает возможность представить в коде требование, чтобы вызывающие его объекты имели какие-то конкретные разрешения.  
  
- Дает возможность представить в коде требование, чтобы вызывающие объекты имели цифровую сигнатуру, позволяя таким образом вызывать защищенный код только пользователям из конкретной организации или веб-узла.  
  
- Вводит ограничения кода во время выполнения, сравнивая предоставленные разрешения каждого участника в стеке вызовов с разрешениями, которые участники должны иметь.  
  
<a name="walking_the_call_stack"></a>
## <a name="walking-the-call-stack"></a>Обход стека вызова  
 Чтобы определить, разрешен ли коду доступ к ресурсу или выполнение операции, система безопасности среды выполнения обходит стек вызовов, сравнивая разрешения, выданные каждому вызывающему объекту, с затребованными разрешениями. Если какой-либо вызывающий объект в стеке вызовов не имеет запрашиваемого разрешения, создается исключение безопасности и ему отказывается в доступе. Обход стека вызовов предназначен для предотвращения отвлекающих атак, когда менее доверенный код вызывает более доверенный и использует его для выполнения неправомочных действий. Требование разрешений от всех вызывающих объектов во время выполнения влияет на производительность, но необходимо для защиты кода от отвлекающих атак со стороны менее доверенного кода. Для оптимизации производительности код может выполнять меньшее количество проходов по стеку. Однако убедитесь, что при этом не предоставляются слабые места в системе безопасности.  
  
 На рисунке ниже показан обход стека, происходящий, когда метод сборки A4 требует, чтобы вызывающие его объекты обладали разрешением P.  
  
 ![Проверка стека управления доступом для кода](media/slide-10a.gif "slide_10a")
  
<a name="related_topics"></a>
## <a name="related-articles"></a>Связанные статьи
  
|Заголовок|Описание|  
|-----------|-----------------|  
|[Основы управления доступом для кода](code-access-security-basics.md)|Описывается управление доступом для кода и распространенные способы его использования.|  
|[Прозрачный с точки зрения безопасности код, уровень 2](security-transparent-code-level-2.md)|Описывает модель прозрачности безопасности в .NET Framework 4.|  
|[Использование библиотек из не вполне надежного кода](using-libraries-from-partially-trusted-code.md)|Описывается, как предоставить доступ к библиотекам и использовать их из неуправляемого код.|  
|[Основные понятия безопасности](../../standard/security/key-security-concepts.md)|Обзор многих ключевых терминов и принципов, используемых в системе безопасности .NET Framework.|  
|[Безопасность на основе ролей](../../standard/security/role-based-security.md)|Описывается использование безопасности на основе ролей.|  
|[службы шифрования](../../standard/security/cryptographic-services.md)|Описывается использование шифрования в приложениях.|
