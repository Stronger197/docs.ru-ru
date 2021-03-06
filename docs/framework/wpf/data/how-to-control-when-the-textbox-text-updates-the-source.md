---
title: Практическое руководство. Управление обновлением источника из поля TextBox
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- source updates [WPF], timing of
- data binding [WPF], timing of source updates
- timing of source updates [WPF]
ms.assetid: ffb7b96a-351d-4c68-81e7-054033781c64
ms.openlocfilehash: 52f3a8d3a5d78a211367722b3042eb50f6ac36d1
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33557229"
---
# <a name="how-to-control-when-the-textbox-text-updates-the-source"></a>Практическое руководство. Управление обновлением источника из поля TextBox
В этом разделе описывается использование <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> свойства для управления синхронизацией обновлений источника привязки. В этом разделе используются <xref:System.Windows.Controls.TextBox> элемента управления в качестве примера.  
  
## <a name="example"></a>Пример  
 Языковой элемент <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> свойство имеет значение по умолчанию <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> значение <xref:System.Windows.Data.UpdateSourceTrigger.LostFocus>. Это означает, что если приложение имеет <xref:System.Windows.Controls.TextBox> с привязкой к данным <xref:System.Windows.Controls.TextBox>.<xref:System.Windows.Controls.TextBox.Text%2A> свойство, текст, вводимый в <xref:System.Windows.Controls.TextBox> обновляет источник до <xref:System.Windows.Controls.TextBox> теряет фокус (например, при нажатии кнопки с <xref:System.Windows.Controls.TextBox>).  
  
 Источник обновляться по мере ввода, установите <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> привязки <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>. В следующем примере выделенные строки кода показывают, что `Text` свойства обоих <xref:System.Windows.Controls.TextBox> и <xref:System.Windows.Controls.TextBlock> связаны с теми же свойствами источника. <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> Свойство <xref:System.Windows.Controls.TextBox> привязки имеет значение <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>.  
  
 [!code-xaml[SimpleBinding#USTHowTo](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/SimpleBinding/VisualBasic/Page1.xaml?highlight=33-39,41-42)]  
  
 В результате <xref:System.Windows.Controls.TextBlock> отображает текст (поскольку источник изменяется), как пользователь вводит в <xref:System.Windows.Controls.TextBox>, как показано на следующем снимке экрана образца:  
  
 ![Снимок экрана примера простой привязки данных ](../../../../docs/framework/wpf/data/media/databindingsimplebindingsample2.png "DataBindingSimpleBindingSample2")  
  
 Если у вас есть диалоговое окно или редактируемая пользователем форма и требуется отложить обновление источника, пока пользователь не завершит редактирование поля и нажимает кнопку «ОК», можно задать <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> значение привязки в <xref:System.Windows.Data.UpdateSourceTrigger.Explicit>, как показано в следующем примере:  
  
 [!code-xaml[UpdateSource#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml#2)]  
  
 При задании <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> значение <xref:System.Windows.Data.UpdateSourceTrigger.Explicit>, исходное значение изменяется, только когда приложение вызывает <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> метод. В следующем примере демонстрируется вызов <xref:System.Windows.Data.BindingExpression.UpdateSource%2A> для `itemNameTextBox`:  
  
 [!code-csharp[UpdateSource#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/UpdateSource/CSharp/Window1.xaml.cs#1)]
 [!code-vb[UpdateSource#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/UpdateSource/VisualBasic/Window1.xaml.vb#1)]  
  
> [!NOTE]
>  Можно использовать ту же методику для свойств других элементов управления, но имейте в виду, что большинство других свойств имеют значение по умолчанию <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> значение <xref:System.Windows.Data.UpdateSourceTrigger.PropertyChanged>. Дополнительные сведения см. в разделе <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> страницу свойств.  
  
> [!NOTE]
>  <xref:System.Windows.Data.Binding.UpdateSourceTrigger%2A> Свойство имеет дело с обновлениями источника и поэтому относится только к <xref:System.Windows.Data.BindingMode.TwoWay> или <xref:System.Windows.Data.BindingMode.OneWayToSource> привязки. Для <xref:System.Windows.Data.BindingMode.TwoWay> и <xref:System.Windows.Data.BindingMode.OneWayToSource> привязки для работы, исходный объект должен предоставить уведомление об изменениях свойств. Можно изучить примеры, приведенные в этом разделе, для получения дополнительной информации. Кроме того, см. раздел [Реализация уведомления об изменении свойства](../../../../docs/framework/wpf/data/how-to-implement-property-change-notification.md).  
  
## <a name="see-also"></a>См. также  
 [Разделы практического руководства](../../../../docs/framework/wpf/data/data-binding-how-to-topics.md)
