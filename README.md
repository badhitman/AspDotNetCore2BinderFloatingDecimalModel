# ASP.NET Core 2.2 BinderFloatingDecimalModel
Привязчик модели для числовых значений double, float и decimal в ASP.NET Core 2.2

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