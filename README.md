# ASP.NET Core 2.2 BinderFloatingDecimalModel
Привязчик модели в ASP.NET Core 2.2 для числовых значений с плавающей точкой **[double, float или decimal]**

Известная особенность стандартного привязчика модели в ASP.NET Core 2.2 заключается в том, что нельзя использовать типы значений с плавающей запятой.
Все числовые значения встроеный привязчик модели пытается обработать как целочисленные, даже если тип свойства модели объявлен как [double, float или decimal].
Данный привязчик модели исправляет не только эту проблему, но и освобождает пользователя от ограничения использования дробного разделителя (точка или запятая).

Данный привязчик позволяет использовать любой разделитель дроби. Любой разделитель принудительно замениться на системный перед конвертацией.
Кроме того допускается усечённый формат записи чисел. Например: 0,5 и .5 дадут один результат. Равно как и 5.0 == 5. Эта особенность выглядет спорной => можно закомментировать эту часть.

```C#
// Regex FloatSeparator = new Regex(@"[.,]", RegexOptions.Compiled)
if (FloatSeparator.IsMatch(FieldValueAsString))
	FieldValueAsNormalString = "0" + FieldValueAsNormalString + "0";
```

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