# Desafio Dio - Ferramentas de Implantação no Azure



####     Projeto ainda mais completo e abrangente com mais códigos para: Ferramentas de Implantação no Azure

**Introdução**

Este projeto irá guiá-lo pelos fundamentos das ferramentas de implantação no Microsoft Azure, uma plataforma de computação em nuvem que oferece uma ampla gama de serviços para ajudá-lo a construir, implantar e gerenciar seus aplicativos de forma eficiente.



### **Pré-requisitos**

- Uma conta do Microsoft Azure

- O Visual Studio 2019 ou superior

- O .NET Core SDK 3.1 ou superior

  

#### **Instruções**

1. **Crie um novo projeto do Visual Studio.**

2. **Selecione o modelo "Aplicativo Web do ASP.NET Core".**

3. **Nomeie o projeto como "AzureDeploymentToolsInAction".**

4. **Clique em "Criar".**

   

5. #### Adicione os seguintes pacotes NuGet ao projeto:

   

   - Microsoft.Azure.Management.AppService

   - Microsoft.Azure.Management.ResourceManager

     

6. #### Adicione as seguintes classes ao projeto:

   

   - **AppServiceService.cs:** Esta classe fornece métodos para interagir com o serviço App Service do Azure.

   - **ResourceManagerService.cs:** Esta classe fornece métodos para interagir com o serviço Resource Manager do Azure.

     

7. #### **Adicione o seguinte código ao arquivo "Startup.cs":**

   

csharp



```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton<IAppServiceService, AppServiceService>();
    services.AddSingleton<IResourceManagerService, ResourceManagerService>();
}
```



1. #### **Adicione o seguinte código ao arquivo "Controllers/HomeController.cs":**

   

csharp



```csharp
public class HomeController : Controller
{
    private readonly IAppServiceService _appServiceService;
    private readonly IResourceManagerService _resourceManagerService;

    public HomeController(IAppServiceService appServiceService, IResourceManagerService resourceManagerService)
    {
        _appServiceService = appServiceService;
        _resourceManagerService = resourceManagerService;
    }

    public IActionResult Index()
    {
        return View();
    }

    [HttpPost]
    public async Task<IActionResult> CreateWebApp(string resourceGroupName, string webAppName)
    {
        await _appServiceService.CreateWebAppAsync(resourceGroupName, webAppName);

        return RedirectToAction("Index");
    }

    [HttpPost]
    public async Task<IActionResult> ListWebApps(string resourceGroupName)
    {
        var webApps = await _appServiceService.ListWebAppsAsync(resourceGroupName);

        return View("WebApps", webApps);
    }
}
```



1. #### **Execute o projeto.**

   

## **Conclusão**

Este projeto fornece uma base ainda mais sólida para você começar a usar as ferramentas de implantação na nuvem no Microsoft Azure. Você pode usar o serviço App Service para criar e gerenciar aplicativos Web e usar o serviço Resource Manager para listar recursos em seu escopo.


## Consultar

https://learn.microsoft.com/pt-br/azure/app-service/quickstart-python?tabs=flask%2Cwindows%2Cazure-cli%2Cazure-cli-deploy%2Cdeploy-instructions-azportal%2Cterminal-bash%2Cdeploy-instructions-zip-azcli

https://learn.microsoft.com/pt-br/azure/azure-resource-manager/templates/template-tutorial-create-first-template?tabs=azure-powershell

https://learn.microsoft.com/pt-br/azure/logic-apps/automate-build-deployment-standard

https://learn.microsoft.com/pt-br/azure/architecture/hybrid/deployments/solution-deployment-guide-highly-available-kubernetes

https://learn.microsoft.com/pt-br/azure/app-service/deploy-best-practices




