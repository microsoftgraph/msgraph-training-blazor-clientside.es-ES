---
ms.openlocfilehash: 4c021fe8aac9b42ee0984a15e73366ead847ee06
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446980"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="1a5cc-101">Empiece por crear una aplicación Desmontaje web de Blazor.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-101">Start by creating a Blazor WebAssembly app.</span></span>

1. <span data-ttu-id="1a5cc-102">Abra la interfaz de línea de comandos (CLI) en un directorio donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-102">Open your command-line interface (CLI) in a directory where you want to create the project.</span></span> <span data-ttu-id="1a5cc-103">Ejecuta el siguiente comando.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-103">Run the following command.</span></span>

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    <span data-ttu-id="1a5cc-104">El `--auth SingleOrg` parámetro hace que el proyecto generado incluya la configuración para la autenticación con el Plataforma de identidad de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-104">The `--auth SingleOrg` parameter causes the generated project to include configuration for authentication with the Microsoft identity platform.</span></span>

1. <span data-ttu-id="1a5cc-105">Una vez creado el proyecto, compruebe que funciona cambiando el directorio actual al directorio **GraphTutorial** y ejecutando el siguiente comando en la CLI.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-105">Once the project is created, verify that it works by changing the current directory to the **GraphTutorial** directory and running the following command in your CLI.</span></span>

    ```Shell
    dotnet watch run
    ```

1. <span data-ttu-id="1a5cc-106">Abra el explorador y vaya a `https://localhost:5001` .</span><span class="sxs-lookup"><span data-stu-id="1a5cc-106">Open your browser and browse to `https://localhost:5001`.</span></span> <span data-ttu-id="1a5cc-107">Si todo funciona, debería ver un "¡Hola, mundo!"</span><span class="sxs-lookup"><span data-stu-id="1a5cc-107">If everything is working, you should see a "Hello, world!"</span></span> <span data-ttu-id="1a5cc-108">Mensaje.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-108">message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a5cc-109">Si recibe una advertencia de que el certificado de **localhost** no es de confianza, puede usar la CLI de .NET Core para instalar y confiar en el certificado de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-109">If you receive a warning that the certificate for **localhost** is un-trusted you can use the .NET Core CLI to install and trust the development certificate.</span></span> <span data-ttu-id="1a5cc-110">Consulta [Aplicar HTTPS en ASP.NET Core](/aspnet/core/security/enforcing-ssl) para obtener instrucciones para sistemas operativos específicos.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-110">See [Enforce HTTPS in ASP.NET Core](/aspnet/core/security/enforcing-ssl) for instructions for specific operating systems.</span></span>

## <a name="add-nuget-packages"></a><span data-ttu-id="1a5cc-111">Agregar paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="1a5cc-111">Add NuGet packages</span></span>

<span data-ttu-id="1a5cc-112">Antes de seguir, instala algunos paquetes NuGet que usarás más adelante.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-112">Before moving on, install some additional NuGet packages that you will use later.</span></span>

- <span data-ttu-id="1a5cc-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-113">[Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) for making calls to Microsoft Graph.</span></span>
- <span data-ttu-id="1a5cc-114">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) para traducir Windows de zona horaria a identificadores de IANA.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-114">[TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) for translating Windows time zone identifiers to IANA identifiers.</span></span>

1. <span data-ttu-id="1a5cc-115">Ejecute los siguientes comandos en la CLI para instalar las dependencias.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-115">Run the following commands in your CLI to install the dependencies.</span></span>

    ```Shell
    dotnet add package Microsoft.Graph --version 4.0.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a><span data-ttu-id="1a5cc-116">Diseñar la aplicación</span><span class="sxs-lookup"><span data-stu-id="1a5cc-116">Design the app</span></span>

<span data-ttu-id="1a5cc-117">En esta sección, crearás la estructura básica de la interfaz de usuario de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-117">In this section you will create the basic UI structure of the application.</span></span>

1. <span data-ttu-id="1a5cc-118">Quite las páginas de ejemplo generadas por la plantilla.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-118">Remove sample pages generated by the template.</span></span> <span data-ttu-id="1a5cc-119">Elimine los archivos siguientes.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-119">Delete the following files.</span></span>

    - <span data-ttu-id="1a5cc-120">**./Pages/Counter.razor**</span><span class="sxs-lookup"><span data-stu-id="1a5cc-120">**./Pages/Counter.razor**</span></span>
    - <span data-ttu-id="1a5cc-121">**./Pages/FetchData.razor**</span><span class="sxs-lookup"><span data-stu-id="1a5cc-121">**./Pages/FetchData.razor**</span></span>
    - <span data-ttu-id="1a5cc-122">**./Shared/SurveyPrompt.razor**</span><span class="sxs-lookup"><span data-stu-id="1a5cc-122">**./Shared/SurveyPrompt.razor**</span></span>
    - <span data-ttu-id="1a5cc-123">**./wwwroot/sample-data/weather.json**</span><span class="sxs-lookup"><span data-stu-id="1a5cc-123">**./wwwroot/sample-data/weather.json**</span></span>

1. <span data-ttu-id="1a5cc-124">Abra **./wwwroot/index.html** y agregue el siguiente código justo **antes de la** etiqueta de `</body>` cierre.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-124">Open **./wwwroot/index.html** and add the following code just **before** the closing `</body>` tag.</span></span>

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    <span data-ttu-id="1a5cc-125">Esto agrega los [archivos javascript de Bootstrap.](https://getbootstrap.com/docs/4.5/getting-started/introduction/)</span><span class="sxs-lookup"><span data-stu-id="1a5cc-125">This adds the [Bootstrap](https://getbootstrap.com/docs/4.5/getting-started/introduction/) javascript files.</span></span>

1. <span data-ttu-id="1a5cc-126">Abre **./wwwroot/css/app.css** y agrega el siguiente código.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-126">Open **./wwwroot/css/app.css** and add the following code.</span></span>

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. <span data-ttu-id="1a5cc-127">Abra **./Shared/NavMenu.razor** y reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-127">Open **./Shared/NavMenu.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. <span data-ttu-id="1a5cc-128">Abra **./Pages/Index.razor** y reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-128">Open **./Pages/Index.razor** and replace its contents with the following.</span></span>

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. <span data-ttu-id="1a5cc-129">Abra **./Shared/LoginDisplay.razor** y reemplace su contenido por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-129">Open **./Shared/LoginDisplay.razor** and replace its contents with the following.</span></span>

    ```razor
    @using Microsoft.AspNetCore.Components.Authorization
    @using Microsoft.AspNetCore.Components.WebAssembly.Authentication

    @inject NavigationManager Navigation
    @inject SignOutSessionStateManager SignOutManager

    <AuthorizeView>
        <Authorized>
            <a class="text-decoration-none" data-toggle="dropdown" href="#" role="button">
                <img src="/img/no-profile-photo.png" class="nav-profile-photo rounded-circle align-self-center mr-2">
            </a>
            <div class="dropdown-menu dropdown-menu-right">
                <h5 class="dropdown-item-text mb-0">@context.User.Identity.Name</h5>
                <p class="dropdown-item-text text-muted mb-0">placeholder@contoso.com</p>
                <div class="dropdown-divider"></div>
                <button class="dropdown-item" @onclick="BeginLogout">Log out</button>
            </div>
        </Authorized>
        <NotAuthorized>
            <a href="authentication/login">Log in</a>
        </NotAuthorized>
    </AuthorizeView>

    @code{
        private async Task BeginLogout(MouseEventArgs args)
        {
            await SignOutManager.SetSignOutState();
            Navigation.NavigateTo("authentication/logout");
        }
    }
    ```

1. <span data-ttu-id="1a5cc-130">Cree un nuevo directorio en **el directorio ./wwwroot** denominado **img**.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-130">Create a new directory in the **./wwwroot** directory named **img**.</span></span> <span data-ttu-id="1a5cc-131">Agregue un archivo de imagen de su elección denominado **no-profile-photo.png** en este directorio.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-131">Add an image file of your choosing named **no-profile-photo.png** in this directory.</span></span> <span data-ttu-id="1a5cc-132">Esta imagen se usará como foto del usuario cuando el usuario no tenga ninguna foto en Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-132">This image will be used as the user's photo when the user has no photo in Microsoft Graph.</span></span>

    > [!TIP]
    > <span data-ttu-id="1a5cc-133">Puede descargar la imagen usada en estas capturas de pantalla desde [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span><span class="sxs-lookup"><span data-stu-id="1a5cc-133">You can download the image used in these screenshots from [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).</span></span>

1. <span data-ttu-id="1a5cc-134">Guarde todos los cambios y actualice la página.</span><span class="sxs-lookup"><span data-stu-id="1a5cc-134">Save all of your changes and refresh the page.</span></span>

    ![Una captura de pantalla de la página de inicio rediseñada](./images/create-app-01.png)
