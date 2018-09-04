---
title: Отключение поддержки определения DPI в Visual Studio
description: Обсуждает ограничения конструктор Windows Forms на HDPI-мониторах, а также как запустить Visual Studio как процесс не поддерживают DPI.
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 65c997e12aa033b3b08d32c8ab76372e3c52a803
ms.sourcegitcommit: efff8f331fd9467f093f8ab8d23a203d6ecb5b60
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/02/2018
ms.locfileid: "43467111"
---
# <a name="disable-dpi-awareness-in-visual-studio"></a><span data-ttu-id="66b36-103">Отключение поддержки определения DPI в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66b36-103">Disable DPI-awareness in Visual Studio</span></span>

<span data-ttu-id="66b36-104">Visual Studio является точек на дюйм (DPI) приложения, что означает отображение шкалы автоматически.</span><span class="sxs-lookup"><span data-stu-id="66b36-104">Visual Studio is a dots per inch (DPI) aware application, which means the display scales automatically.</span></span> <span data-ttu-id="66b36-105">Если приложение указано, что он не поддерживает определение DPI, операционная система масштабируется приложение в качестве растрового изображения.</span><span class="sxs-lookup"><span data-stu-id="66b36-105">If an application states that it's not DPI-aware, the operating system scales the application as a bitmap.</span></span> <span data-ttu-id="66b36-106">Это поведение также называется виртуализации точек на ДЮЙМ.</span><span class="sxs-lookup"><span data-stu-id="66b36-106">This behavior is also called DPI virtualization.</span></span> <span data-ttu-id="66b36-107">Приложение по-прежнему считает, что он выполняется на 100% масштабирования или 96 точек на дюйм.</span><span class="sxs-lookup"><span data-stu-id="66b36-107">The application still thinks that it's running at 100% scaling, or 96 dpi.</span></span>

## <a name="windows-forms-designer-on-hdpi-monitors"></a><span data-ttu-id="66b36-108">Конструктор Windows Forms на HDPI-мониторах</span><span class="sxs-lookup"><span data-stu-id="66b36-108">Windows Forms Designer on HDPI monitors</span></span>

<span data-ttu-id="66b36-109">**Конструктор Windows Forms** в Visual Studio не имеет масштабирования.</span><span class="sxs-lookup"><span data-stu-id="66b36-109">The **Windows Forms Designer** in Visual Studio doesn't have scaling support.</span></span> <span data-ttu-id="66b36-110">При открытии некоторых форм, в результате проблем с отображением **конструктор Windows Forms** на большое число точек на дюйм (HDPI) мониторов.</span><span class="sxs-lookup"><span data-stu-id="66b36-110">This causes display issues when you open some forms in the **Windows Forms Designer** on high dots per inch (HDPI) monitors.</span></span> <span data-ttu-id="66b36-111">Например элементы управления могут иметь пересекаются, как показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="66b36-111">For examples, controls can appear to overlap as shown in the following image:</span></span>

![Конструктор Windows Forms на мониторе HDPI](media/disable-dpi-awareness-visual-studio/win-forms-designer-hdpi.png)

<span data-ttu-id="66b36-113">В Visual Studio 2017 версии 15,8 и более поздние версии, при открытии формы в **конструктор Windows Forms** на мониторе HDPI, Visual Studio отображает желтый, информационные панели в верхней части конструктора:</span><span class="sxs-lookup"><span data-stu-id="66b36-113">In Visual Studio 2017 version 15.8 and later, when you open a form in the **Windows Forms Designer** on an HDPI monitor, Visual Studio displays a yellow informational bar at the top of the designer:</span></span>

![Информационные панели в Visual Studio, чтобы перезагрузить компьютер в режиме не поддерживают DPI](media/disable-dpi-awareness-visual-studio/scaling-gold-bar.png)

<span data-ttu-id="66b36-115">Считывает сообщение **масштабирование на главном экране равен 200% (192 dpi). Это может вызвать проблемы отрисовки в окне конструктора.**</span><span class="sxs-lookup"><span data-stu-id="66b36-115">The message reads **Scaling on your main display is set to 200% (192 dpi). This might cause rendering problems in the designer window.**</span></span>

<span data-ttu-id="66b36-116">Если вы не работают в конструкторе, не требуется для настройки макета формы можно игнорировать информационные панели и продолжить работу в редакторе кода или в других типах конструкторов.</span><span class="sxs-lookup"><span data-stu-id="66b36-116">If you aren't working in the designer and don't need to adjust the layout of your form, you can ignore the informational bar and continue working in the code editor or in other types of designers.</span></span> <span data-ttu-id="66b36-117">Только **конструктор Windows Forms** снижается.</span><span class="sxs-lookup"><span data-stu-id="66b36-117">Only the **Windows Forms Designer** is affected.</span></span> <span data-ttu-id="66b36-118">Если вам нужно работать в **конструктор Windows Forms**, следующий раздел поможет вам [решить проблему](#to-resolve-the-problem).</span><span class="sxs-lookup"><span data-stu-id="66b36-118">If you do need to work in the **Windows Forms Designer**, the next section helps you [resolve the problem](#to-resolve-the-problem).</span></span>

## <a name="to-resolve-the-problem"></a><span data-ttu-id="66b36-119">Чтобы устранить эту проблему</span><span class="sxs-lookup"><span data-stu-id="66b36-119">To resolve the problem</span></span>

<span data-ttu-id="66b36-120">Существует три варианта для устранения проблемы отображения.</span><span class="sxs-lookup"><span data-stu-id="66b36-120">There are three options to resolve the display problem.</span></span>

### <a name="restart-visual-studio-as-a-dpi-unaware-process"></a><span data-ttu-id="66b36-121">Перезапустите Visual Studio как процесс не поддерживают DPI</span><span class="sxs-lookup"><span data-stu-id="66b36-121">Restart Visual Studio as a DPI-unaware process</span></span>

<span data-ttu-id="66b36-122">Как процесс не поддерживают DPI можно перезапустить Visual Studio, выбрав параметр на желтый информационные панели.</span><span class="sxs-lookup"><span data-stu-id="66b36-122">You can restart Visual Studio as a DPI-unaware process by selecting the option on the yellow informational bar.</span></span> <span data-ttu-id="66b36-123">Это предпочтительный способ устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="66b36-123">This is the preferred way of resolving the problem.</span></span>

<span data-ttu-id="66b36-124">При запуске Visual Studio как процесс не поддерживают DPI, устранения проблем макет конструктора, но шрифты могут быть нечеткими.</span><span class="sxs-lookup"><span data-stu-id="66b36-124">When Visual Studio runs as a DPI-unaware process, the designer layout issues are resolved, but fonts may appear blurry.</span></span> <span data-ttu-id="66b36-125">Visual Studio отображает различные желтый информационное сообщение, когда он выполняется как процесс не поддерживают DPI, — говорит **Visual Studio выполняется как процесс не поддерживают DPI. Конструкторы WPF и XAML могут отображаться неправильно.**</span><span class="sxs-lookup"><span data-stu-id="66b36-125">Visual Studio displays a different yellow informational message when it runs as a DPI-unaware process that says **Visual Studio is running as a DPI-unaware process. WPF and XAML designers might not display correctly.**</span></span> <span data-ttu-id="66b36-126">Информационные панели также предоставляет возможность **перезапустите Visual Studio, как поддерживающее DPI процесс**.</span><span class="sxs-lookup"><span data-stu-id="66b36-126">The informational bar also provides an option to **Restart Visual Studio as a DPI-aware process**.</span></span>

> [!NOTE]
> - <span data-ttu-id="66b36-127">Если извлечения окна инструментов в Visual Studio при выборе перезагрузите компьютер как процесс не поддерживают DPI, может измениться положения этих окон инструментов.</span><span class="sxs-lookup"><span data-stu-id="66b36-127">If you had undocked tool windows in Visual Studio when you selected the option to restart as a DPI-unaware process, the position of those tool windows may change.</span></span>
> - <span data-ttu-id="66b36-128">Если вы используете профиль Visual Basic по умолчанию, или у вас есть **сохранять новые проекты при создании** параметр выбран в **средства** > **параметры**  >  **Проекты и решения**, Visual Studio не удается восстановить проект после его перезапуска, как процесс не поддерживают DPI.</span><span class="sxs-lookup"><span data-stu-id="66b36-128">If you use the default Visual Basic profile, or if you have the **Save new projects when created** option deselected in **Tools** > **Options** > **Projects and Solutions**, Visual Studio cannot reopen your project when it restarts as a DPI-unaware process.</span></span> <span data-ttu-id="66b36-129">Тем не менее, можно открыть проект, выбрав его в разделе **файл** > **последние проекты и решения**.</span><span class="sxs-lookup"><span data-stu-id="66b36-129">However, you can open the project by selecting it under **File** > **Recent Projects and Solutions**.</span></span>

<span data-ttu-id="66b36-130">Очень важно перезапустить Visual Studio как поддерживающее DPI процесс при завершении работы **конструктор Windows Forms**.</span><span class="sxs-lookup"><span data-stu-id="66b36-130">It's important to restart Visual Studio as a DPI-aware process when you're finished working in the **Windows Forms Designer**.</span></span> <span data-ttu-id="66b36-131">Когда он выполняется как процесс не поддерживают DPI, можно, выглядели нечеткими шрифты и могут возникнуть проблемы в других конструкторах например **конструктор XAML**.</span><span class="sxs-lookup"><span data-stu-id="66b36-131">When it's running as a DPI-unaware process, fonts can look blurry and you may see issues in other designers such as the **XAML Designer**.</span></span> <span data-ttu-id="66b36-132">Если вы закроете и снова откройте Visual Studio при работе в режиме не поддерживают DPI, он становится дюйм еще раз.</span><span class="sxs-lookup"><span data-stu-id="66b36-132">If you close and reopen Visual Studio when it's running in DPI-unaware mode, it becomes DPI-aware again.</span></span> <span data-ttu-id="66b36-133">Можно также щелкнуть **перезапустите Visual Studio, как поддерживающее DPI процесс** параметр на информационные панели.</span><span class="sxs-lookup"><span data-stu-id="66b36-133">You can also click the **Restart Visual Studio as a DPI-aware process** option in the informational bar.</span></span>

### <a name="add-a-registry-entry"></a><span data-ttu-id="66b36-134">Добавьте параметр реестра</span><span class="sxs-lookup"><span data-stu-id="66b36-134">Add a registry entry</span></span>

<span data-ttu-id="66b36-135">Visual Studio можно пометить как не поддерживающие точек на ДЮЙМ, путем изменения реестра.</span><span class="sxs-lookup"><span data-stu-id="66b36-135">You can mark Visual Studio as DPI-unaware by modifying the registry.</span></span> <span data-ttu-id="66b36-136">Откройте **редактора реестра** и добавить запись **NT\CurrentVersion\AppCompatFlags\Layers этот** подраздел:</span><span class="sxs-lookup"><span data-stu-id="66b36-136">Open **Registry Editor** and add an entry to the **HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags\Layers** subkey:</span></span>

<span data-ttu-id="66b36-137">**Запись**: % ProgramFiles (x86) %\Microsoft Visual Studio\2017\your-edition\Common7\IDE\devenv.exe</span><span class="sxs-lookup"><span data-stu-id="66b36-137">**Entry**: %ProgramFiles(x86)%\Microsoft Visual Studio\2017\your-edition\Common7\IDE\devenv.exe</span></span>

<span data-ttu-id="66b36-138">**Тип**: REG_SZ</span><span class="sxs-lookup"><span data-stu-id="66b36-138">**Type**: REG_SZ</span></span>

<span data-ttu-id="66b36-139">**Значение**: DPIUNAWARE</span><span class="sxs-lookup"><span data-stu-id="66b36-139">**Value**: DPIUNAWARE</span></span>

> [!NOTE]
> <span data-ttu-id="66b36-140">Visual Studio остается в режиме не поддерживают DPI, пока вы не удалите запись в реестр.</span><span class="sxs-lookup"><span data-stu-id="66b36-140">Visual Studio remains in DPI-unaware mode until you remove the registry entry.</span></span>

### <a name="set-your-display-scaling-setting-to-100"></a><span data-ttu-id="66b36-141">Настройте дисплей масштабирование параметр до 100%</span><span class="sxs-lookup"><span data-stu-id="66b36-141">Set your display scaling setting to 100%</span></span>

<span data-ttu-id="66b36-142">Для применения вашего экрана, масштабирование параметр до 100% в Windows 10 введите **параметры отображения** в панели поиска, а затем выберите задач **изменению параметров отображения**.</span><span class="sxs-lookup"><span data-stu-id="66b36-142">To set your display scaling setting to 100% in Windows 10, type **display settings** in the task bar search box, and then select **Change display settings**.</span></span> <span data-ttu-id="66b36-143">В **параметры** окне **изменить размер текста, приложений и других элементов** для **100%**.</span><span class="sxs-lookup"><span data-stu-id="66b36-143">In the **Settings** window, set **Change the size of text, apps, and other items** to **100%**.</span></span>

<span data-ttu-id="66b36-144">Настройка вашего экрана, масштабирование до 100% может быть нежелательно, так как он может сделать пользовательский интерфейс слишком мал, чтобы можно было использовать.</span><span class="sxs-lookup"><span data-stu-id="66b36-144">Setting your display scaling to 100% may be undesirable, because it can make the user interface too small to be usable.</span></span>

## <a name="see-also"></a><span data-ttu-id="66b36-145">См. также</span><span class="sxs-lookup"><span data-stu-id="66b36-145">See also</span></span>

- [<span data-ttu-id="66b36-146">Автоматическое масштабирование в Windows Forms</span><span class="sxs-lookup"><span data-stu-id="66b36-146">Automatic scaling in Windows Forms</span></span>](automatic-scaling-in-windows-forms.md)