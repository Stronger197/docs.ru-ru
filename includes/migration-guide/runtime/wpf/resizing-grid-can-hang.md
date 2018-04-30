### <a name="resizing-a-grid-can-hang"></a><span data-ttu-id="9580f-101">Изменение размеров сетки может привести к зависанию</span><span class="sxs-lookup"><span data-stu-id="9580f-101">Resizing a Grid can hang</span></span>

|   |   |
|---|---|
|<span data-ttu-id="9580f-102">Подробные сведения</span><span class="sxs-lookup"><span data-stu-id="9580f-102">Details</span></span>|<span data-ttu-id="9580f-103">При изменении макета <code>T:System.Windows.Controls.Grid</code> в следующих обстоятельствах может возникать бесконечный цикл:</span><span class="sxs-lookup"><span data-stu-id="9580f-103">An infinite loop can occur during layout of a <code>T:System.Windows.Controls.Grid</code> under the following circumstances:</span></span><ul><li><span data-ttu-id="9580f-104">Определения строк содержат два атрибута \*-rows, которые объявляют значения MinHeight и MaxHeight.</span><span class="sxs-lookup"><span data-stu-id="9580f-104">Row definitions contain two \*-rows, both declaring a MinHeight and a MaxHeight.</span></span></li><li><span data-ttu-id="9580f-105">Содержимое \*-rows не превышает ограничение, устанавливаемое соответствующим значением MaxHeight.</span><span class="sxs-lookup"><span data-stu-id="9580f-105">Content of the \*-rows doesn't exceed the corresponding MaxHeight</span></span></li><li><span data-ttu-id="9580f-106">Первое значение MinHeight (плюс любые другие фиксированные или автоматические строки) превышает доступную высоту сетки.</span><span class="sxs-lookup"><span data-stu-id="9580f-106">The Grid's available height is exceeded by the first MinHeight (plus any other fixed or Auto rows)</span></span></li><li><span data-ttu-id="9580f-107">Приложение предназначено для .NET 4.7 или использует алгоритм выделения версии 4.7, включенный с помощью параметра <code>Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=false</code>.</span><span class="sxs-lookup"><span data-stu-id="9580f-107">The app targets .Net 4.7, or opts in to the 4.7 allocation algorithm by setting <code>Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=false</code></span></span></li></ul><span data-ttu-id="9580f-108">Кроме того, цикл может возникать при наличии более двух строк или в аналогичных случаях для столбцов. Проблема устранена в .NET 4.7.1.</span><span class="sxs-lookup"><span data-stu-id="9580f-108">The loop would also happen with more than two rows, or in the analogous case for columns.The issue is fixed in .Net 4.7.1.</span></span>|
|<span data-ttu-id="9580f-109">Предложение</span><span class="sxs-lookup"><span data-stu-id="9580f-109">Suggestion</span></span>|<span data-ttu-id="9580f-110">Выполните обновление до .NET 4.7.1.</span><span class="sxs-lookup"><span data-stu-id="9580f-110">Upgrade to .Net 4.7.1.</span></span>  <span data-ttu-id="9580f-111">Кроме того, если вам не требуется алгоритм выделения версии 4.7, вы можете использовать следующий параметр конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9580f-111">Alternatively, if you don't need the 4.7 allocation algorithm you can use the following configuration setting:</span></span><pre><code class="language-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Controls.Grid.StarDefinitionsCanExceedAvailableSpace=true&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>|
|<span data-ttu-id="9580f-112">Область</span><span class="sxs-lookup"><span data-stu-id="9580f-112">Scope</span></span>|<span data-ttu-id="9580f-113">Пограничный случай</span><span class="sxs-lookup"><span data-stu-id="9580f-113">Edge</span></span>|
|<span data-ttu-id="9580f-114">Версия</span><span class="sxs-lookup"><span data-stu-id="9580f-114">Version</span></span>|<span data-ttu-id="9580f-115">4.7</span><span class="sxs-lookup"><span data-stu-id="9580f-115">4.7</span></span>|
|<span data-ttu-id="9580f-116">Тип</span><span class="sxs-lookup"><span data-stu-id="9580f-116">Type</span></span>|<span data-ttu-id="9580f-117">Среда выполнения</span><span class="sxs-lookup"><span data-stu-id="9580f-117">Runtime</span></span>|
