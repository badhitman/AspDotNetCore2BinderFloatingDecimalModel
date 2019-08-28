# ASP.NET Core 2.2 BinderFloatingDecimalModel
Привязчик модели для числовых значений double, float и decimal в ASP.NET Core 2.2

Позволяет в формах использовать любой разделитель дроби. Можно использовать либо точку либо запятую. Любой разделитель принудительно замениться на системный перед конвертацией.
Допускается сокращённый формат записи чисел. Например: 0,5 и .5 дадут один результат

Отдельного внимания требует шаблон регулярного выражения предполагаемого значения. Файл: **CustomFloatingModelBinder.cs**
```C#
protected readonly Regex FloatPattern = new Regex(@"^(-?)[0-9]*(?:[.,][0-9]*)?$", RegexOptions.Compiled);
```
Проверьте его что бы оно отвечало поставленым задачам в вашем контексте

Использование:
```C#
using AspDotNetCore2BinderFloatingDecimalModel;
// ...
public void ConfigureServices(IServiceCollection services)
{
	// ...
	services.AddMvc(opts =>
	{
		opts.ModelBinderProviders.Insert(0, new CustomDecimalModelBinderProvider());
	}).SetCompatibilityVersion(CompatibilityVersion.Version_2_2);
}
```