---
title: Практическое руководство. Сокрытие элемента управления во время выполнения
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- controls [Windows Forms], making invisible at run time
- invisible controls
- user controls [Windows Forms], invisible
- custom controls [Windows Forms], invisible
- run time [Windows Forms], making controls invisible
ms.assetid: 69eb2e72-32f5-4f79-a157-c2c5f60c1628
ms.openlocfilehash: 51e804c7f01b55ed7504837042b6c32bf47d9405
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/04/2018
ms.locfileid: "33532416"
---
# <a name="how-to-make-your-control-invisible-at-run-time"></a>Практическое руководство. Сокрытие элемента управления во время выполнения
Бывают случаи, когда может потребоваться создать пользовательский элемент управления, который остается невидимым во время выполнения. Например элемент управления, выполняющий функции будильника может быть невидимой, за исключением случаев, когда будильника. Это делается путем присвоения свойству легко <xref:System.Windows.Forms.Control.Visible%2A> свойство. Если <xref:System.Windows.Forms.Control.Visible%2A> свойство `true`, элемент управления отображается в обычном режиме. Если `false`, элемент управления будет скрыт. Несмотря на то, что код в элемент управления может выполняться при скрытии, вы не сможете взаимодействовать с элементом управления через пользовательский интерфейс. Если вы хотите создать невидимом элементе управления, который реагирует на пользовательский ввод (например, щелчки мышью), следует создать прозрачный элемент управления. Дополнительные сведения см. в разделе [предоставления элемента управления прозрачный фон](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md).  
  
### <a name="to-make-your-control-invisible-at-run-time"></a>Чтобы скрыть элемент управления во время выполнения  
  
1.  Задайте для свойства <xref:System.Windows.Forms.Control.Visible%2A> значение `false`.  
  
    ```vb  
    ' To set the Visible property from within your object's own code.  
    Me.Visible = False  
    ' To set the Visible property from another object.  
    myControl1.Visible = False  
    ```  
  
    ```csharp  
    // To set the Visible property from within your object's own code.  
    this.Visible = false;  
    // To set the Visible property from another object.  
    myControl1.Visible = false;  
    ```  
  
## <a name="see-also"></a>См. также  
 <xref:System.Windows.Forms.Control.Visible%2A>  
 [Разработка пользовательских элементов управления Windows Forms в .NET Framework](../../../../docs/framework/winforms/controls/developing-custom-windows-forms-controls.md)  
 [Практическое руководство. Установка степени прозрачности фона элемента управления](../../../../docs/framework/winforms/controls/how-to-give-your-control-a-transparent-background.md)
