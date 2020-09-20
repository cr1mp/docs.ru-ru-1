---
title: Обзор асинхронной модели, основанной на событиях
description: Обзор асинхронных моделей на основе событий (EAP) в .NET, которые предоставляют преимущества многопоточных приложений и скрывают некоторые сложности в проектировании.
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Event-based Asynchronous Pattern
- ProgressChangedEventArgs class
- BackgroundWorker component
- events [.NET Framework], asynchronous
- Asynchronous Pattern
- AsyncOperationManager class
- threading [.NET Framework], asynchronous features
- AsyncOperation class
- AsyncCompletedEventArgs class
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
ms.openlocfilehash: 18fbdb29e5a1fb02601dea00964538144c07122c
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768863"
---
# <a name="event-based-asynchronous-pattern-overview"></a>Обзор асинхронной модели, основанной на событиях
Приложениям, выполняющим множество задач одновременно и при этом активно реагирующим на действия пользователя, часто требуется структура, использующая несколько потоков. Пространство имен <xref:System.Threading> предоставляет все необходимые средства для создания высокопроизводительных многопоточных приложений, однако для эффективного использования этих средств требуется значительный опыт в области многопоточной программной инженерии. Для относительно простых многопоточных приложений компонент <xref:System.ComponentModel.BackgroundWorker> предоставляет прямолинейное решение. Для более сложных асинхронных приложений рекомендуется реализовать класс, который соответствует асинхронной модели на основе событий.  
  
 Асинхронная модель на основе событий позволяет использовать преимущества многопоточных приложений и устраняет многие сложности, присущие многопоточности. Используя класс, поддерживающий такую модель, вы можете:  
  
- выполнять задачи, занимающие много времени, такие как загрузки и операции с базами данных, "в фоновом режиме" без прерывания работы приложения;  
  
- выполнять несколько операций одновременно, получая уведомления о завершении каждой из них;  
  
- ожидать освобождения ресурсов без остановки ("блокирования") приложения;  
  
- взаимодействовать с ожидающими асинхронными операциями с использованием привычной модели событий и делегатов. Дополнительные сведения об использовании обработчиков событий и делегатов см. в статье [События](../events/index.md).  
  
 Класс, который поддерживает асинхронную модель на основе событий, будет иметь один или несколько методов с именем _MethodName_**Async**. Эти методы могут копировать синхронные версии, выполняющие ту же операцию в текущем потоке. Этот класс может содержать событие _MethodName_**Completed**, а также метод _MethodName_**AsyncCancel** (или просто **CancelAsync**).  
  
 <xref:System.Windows.Forms.PictureBox> — это типичный компонент, поддерживающий асинхронную модель на основе событий. Вы можете загрузить изображение синхронно, вызвав его метод <xref:System.Windows.Forms.PictureBox.Load%2A>, но если изображение имеет большой размер или используется медленное подключение к сети, ваше приложение перестанет отвечать до завершения операции загрузки и возврата вызова <xref:System.Windows.Forms.PictureBox.Load%2A>.  
  
 Если вы хотите, чтобы приложение продолжало работать во время загрузки изображения, можно вызвать метод <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> и обработать событие <xref:System.Windows.Forms.PictureBox.LoadCompleted> так, как и любое другое. При вызове метода <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> ваше приложение продолжит выполняться, пока загрузка идет в отдельном потоке ("в фоновом режиме"). После завершения операции загрузки изображения вызывается ваш обработчик событий, который может изучить параметр <xref:System.ComponentModel.AsyncCompletedEventArgs>, чтобы определить, была ли загрузка успешной.  
  
 Асинхронная модель на основе событий требует наличия возможности отмены асинхронной операции, и элемент управления <xref:System.Windows.Forms.PictureBox> позволяет выполнить это требование с помощью метода <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>. При вызове <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> отправляется запрос на остановку ожидающей загрузки, а после отмены задачи возникает событие <xref:System.Windows.Forms.PictureBox.LoadCompleted>.  
  
> [!CAUTION]
> Загрузка может закончиться одновременно с получением запроса <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>, поэтому <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> может не отражать отмену запроса. Это называется *состоянием гонки* и является распространенной проблемой в многопоточном программировании. Дополнительные сведения о проблемах многопоточного программирования см. в разделе [Рекомендации по работе с потоками](../threading/managed-threading-best-practices.md).  
  
## <a name="characteristics-of-the-event-based-asynchronous-pattern"></a>Характеристики асинхронной модели на основе событий  
 Асинхронная модель на основе событий может принимать разную форму в зависимости от операций, поддерживаемых определенным классом. Простейшие классы могут иметь один метод _MethodName_**Async** и одно соответствующее ему событие _MethodName_**Completed**. Более сложные классы будут содержать несколько методов _MethodName_**Async** с соответствующими событиями _MethodName_**Completed**, а также синхронные версии этих методов. Классы также могут поддерживать отмену, составление отчетов о ходе работы и добавочные результаты для каждого асинхронного метода.  
  
 Асинхронный метод также поддерживает несколько ожидающих вызовов (несколько одновременно выполняемых вызовов), позволяя вашему коду вызывать его любое число раз, прежде чем он выполнит другие ожидающие операции. Для корректного разрешения данной ситуации вашему приложению может потребоваться отслеживать выполнение каждой операции.  
  
### <a name="examples-of-the-event-based-asynchronous-pattern"></a>Примеры для асинхронной модели на основе событий  
 Компоненты <xref:System.Media.SoundPlayer> и <xref:System.Windows.Forms.PictureBox> представляют простые реализации асинхронной модели на основе событий. Компоненты <xref:System.Net.WebClient> и <xref:System.ComponentModel.BackgroundWorker> представляют более сложные реализации асинхронной модели на основе событий.  
  
 Ниже приведен пример объявления класса в соответствии с данной моделью:  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer
    Public Sub Method2(ByVal param As Double)
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 Вымышленный класс `AsyncExample` имеет два метода, которые поддерживают как синхронные, так и асинхронные вызовы. Синхронные перегрузки работают аналогично вызову любого метода и выполняют операцию в вызывающем потоке; если выполнение операции требует много времени, перед возвратом вызова может возникнуть значительная задержка. Асинхронные перегрузки запустят операцию в другом потоке и затем немедленно выполнят возврат, позволяя вызывающему потоку продолжить работу, пока операция выполняется "в фоновом режиме".  
  
### <a name="asynchronous-method-overloads"></a>Асинхронные перегрузки методов  
 Для асинхронных операций существует две перегрузки: с одним вызовом и с несколькими вызовами. Различить две этих формы можно по их сигнатурам методов: форма с несколькими вызовами имеет дополнительный параметр с именем `userState`. Эта форма позволяет коду вызвать `Method1Async(string param, object userState)` несколько раз, не ожидая завершения ожидающих асинхронных операций. С другой стороны, если попытаться вызвать `Method1Async(string param)` до завершения предыдущего вызова, метод выдает исключение <xref:System.InvalidOperationException>.  
  
 Параметр `userState` для перегрузок с несколькими вызовами позволяет вам различать асинхронные операции. Вы указываете уникальное значение (например, GUID или хэш-код) для каждого вызова `Method1Async(string param, object userState)`, что позволяет обработчику событий после завершения каждой из операций определить, какой экземпляр этой операции сообщил о своем завершении.  
  
### <a name="tracking-pending-operations"></a>Отслеживание ожидающих операций  
 Если вы используете перегрузки с несколькими вызовами, вашему коду потребуется отслеживать объекты `userState` (идентификаторы) для ожидающих задач. Для каждого вызова `Method1Async(string param, object userState)` обычно создается новый уникальный объект `userState`, который добавляется в коллекцию. Когда задача, соответствующая этому объекту `userState`, выдает событие выполнения, реализация метода выполнения проверяет <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=nameWithType> и удаляет его из вашей коллекции. При таком использовании параметр `userState` играет роль идентификатора задачи.  
  
> [!NOTE]
> Вам следует внимательно следить за тем, чтобы значение, заданное для `userState` в ваших вызовах перегрузок с несколькими вызовами, было уникальным. В случае неуникальных идентификаторов задач асинхронный класс выдает исключение <xref:System.ArgumentException>.  
  
### <a name="canceling-pending-operations"></a>Отмена ожидающих операций  
 Важно иметь возможность отменить асинхронные операции в любое время до их завершения. Классы, реализующие асинхронную модель на основе событий, будут иметь метод `CancelAsync` (если асинхронный метод всего один) или методы _MethodName_**AsyncCancel** (если асинхронных методов несколько).  
  
 Методы, допускающие несколько вызовов, принимают параметр `userState`, который можно использовать для отслеживания времени существования каждой задачи. `CancelAsync` принимает параметр `userState`, позволяющий отменить определенные ожидающие задачи.  
  
 Методы, которые одновременно поддерживают только одну ожидающую операцию, такие как `Method1Async(string param)`, не допускают отмену.  
  
### <a name="receiving-progress-updates-and-incremental-results"></a>Получение обновлений хода выполнения и добавочных результатов  
 Класс, поддерживающий асинхронную модель на основе событий, может дополнительно предоставлять событие для отслеживания хода выполнения и добавочных результатов. Обычно оно имеет имя `ProgressChanged` или _MethodName_**ProgressChanged**, а соответствующий обработчик событий принимает параметр <xref:System.ComponentModel.ProgressChangedEventArgs>.  
  
 Обработчик событий для события `ProgressChanged` может проверить свойство <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=nameWithType>, чтобы определить, какой процент асинхронной задачи уже выполнен. Это свойство находится в диапазоне от 0 до 100 и может использоваться для обновления свойства <xref:System.Windows.Forms.ProgressBar.Value%2A> элемента <xref:System.Windows.Forms.ProgressBar>. Если имеется несколько ожидающих асинхронных операций, вы можете использовать свойство <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=nameWithType>, чтобы определить, какая операция сообщает о ходе выполнения.  
  
 Некоторые классы могут предоставлять добавочные результаты по мере выполнения асинхронных операций. Эти результаты будут сохранены в классе, который является производным от <xref:System.ComponentModel.ProgressChangedEventArgs>, и будут иметь вид свойств в производном классе. Вы можете получить доступ к этим результатам в обработчике событий для события `ProgressChanged` точно так же, как стали бы получать доступ к свойству <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>. Если имеется несколько ожидающих асинхронных операций, вы можете использовать свойство <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A>, чтобы определить, какая операция выдает добавочные результаты.  
  
## <a name="see-also"></a>См. также

- <xref:System.ComponentModel.ProgressChangedEventArgs>
- <xref:System.ComponentModel.BackgroundWorker>
- <xref:System.ComponentModel.AsyncCompletedEventArgs>
- [Практическое руководство. Использование компонентов, поддерживающих асинхронную модель, основанную на событиях](how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)
- [Практическое руководство. Фоновое выполнение операции](../../framework/winforms/controls/how-to-run-an-operation-in-the-background.md)
- [Практическое руководство. Реализация формы, в которой выполняется фоновая операция](../../framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)
- [Асинхронная модель на основе событий (EAP)](event-based-asynchronous-pattern-eap.md)
- [Рекомендации по реализации асинхронной модели, основанной на событиях](best-practices-for-implementing-the-event-based-asynchronous-pattern.md)
- [Определение, когда следует реализовать асинхронную модель, основанную на событиях](deciding-when-to-implement-the-event-based-asynchronous-pattern.md)
