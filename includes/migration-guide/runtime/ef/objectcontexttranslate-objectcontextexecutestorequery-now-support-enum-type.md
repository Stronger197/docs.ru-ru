### <a name="objectcontexttranslate-and-objectcontextexecutestorequery-now-support-enum-type"></a>ObjectContext.Translate и ObjectContext.ExecuteStoreQuery теперь поддерживают тип перечисления

|   |   |
|---|---|
|Подробные сведения|В .NET Framework 4.0 универсальный параметр <code>T</code> методов <code>ObjectContext.Translate</code> и <code>ObjectContext.ExecuteStoreQuery</code> не мог иметь тип перечисления. Теперь этот сценарий поддерживается.|
|Предложение|Если метод Translate или ExecuteStoreQuery вызывался для типа перечисления в .NET Framework 4.0, возвращалось значение "0". Если такое поведение было желательным, вызовы следовало заменять константой 0 (или его эквивалентом перечисления).|
|Область|Пограничный случай|
|Версия|4.5|
|Тип|Среда выполнения|
|Затронутые API|<ul><li><xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.Translate%60%601(System.Data.Common.DbDataReader,System.String,System.Data.Objects.MergeOption)?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.Object[])?displayProperty=nameWithType></li><li><xref:System.Data.Objects.ObjectContext.ExecuteStoreQuery%60%601(System.String,System.String,System.Data.Objects.MergeOption,System.Object[])?displayProperty=nameWithType></li></ul>|

