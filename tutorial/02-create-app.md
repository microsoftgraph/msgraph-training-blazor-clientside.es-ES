---
ms.openlocfilehash: 4c021fe8aac9b42ee0984a15e73366ead847ee06
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446980"
---
<!-- markdownlint-disable MD002 MD041 -->

Empiece por crear una aplicación Desmontaje web de Blazor.

1. Abra la interfaz de línea de comandos (CLI) en un directorio donde desee crear el proyecto. Ejecuta el siguiente comando.

    ```Shell
    dotnet new blazorwasm --auth SingleOrg -o GraphTutorial
    ```

    El `--auth SingleOrg` parámetro hace que el proyecto generado incluya la configuración para la autenticación con el Plataforma de identidad de Microsoft.

1. Una vez creado el proyecto, compruebe que funciona cambiando el directorio actual al directorio **GraphTutorial** y ejecutando el siguiente comando en la CLI.

    ```Shell
    dotnet watch run
    ```

1. Abra el explorador y vaya a `https://localhost:5001` . Si todo funciona, debería ver un "¡Hola, mundo!" Mensaje.

> [!IMPORTANT]
> Si recibe una advertencia de que el certificado de **localhost** no es de confianza, puede usar la CLI de .NET Core para instalar y confiar en el certificado de desarrollo. Consulta [Aplicar HTTPS en ASP.NET Core](/aspnet/core/security/enforcing-ssl) para obtener instrucciones para sistemas operativos específicos.

## <a name="add-nuget-packages"></a>Agregar paquetes NuGet

Antes de seguir, instala algunos paquetes NuGet que usarás más adelante.

- [Microsoft.Graph](https://www.nuget.org/packages/Microsoft.Graph/) para realizar llamadas a Microsoft Graph.
- [TimeZoneConverter](https://github.com/mj1856/TimeZoneConverter) para traducir Windows de zona horaria a identificadores de IANA.

1. Ejecute los siguientes comandos en la CLI para instalar las dependencias.

    ```Shell
    dotnet add package Microsoft.Graph --version 4.0.0
    dotnet add package TimeZoneConverter
    ```

## <a name="design-the-app"></a>Diseñar la aplicación

En esta sección, crearás la estructura básica de la interfaz de usuario de la aplicación.

1. Quite las páginas de ejemplo generadas por la plantilla. Elimine los archivos siguientes.

    - **./Pages/Counter.razor**
    - **./Pages/FetchData.razor**
    - **./Shared/SurveyPrompt.razor**
    - **./wwwroot/sample-data/weather.json**

1. Abra **./wwwroot/index.html** y agregue el siguiente código justo **antes de la** etiqueta de `</body>` cierre.

    :::code language="html" source="../demo/GraphTutorial/wwwroot/index.html" id="BootStrapJSSnippet":::

    Esto agrega los [archivos javascript de Bootstrap.](https://getbootstrap.com/docs/4.5/getting-started/introduction/)

1. Abre **./wwwroot/css/app.css** y agrega el siguiente código.

    :::code language="css" source="../demo/GraphTutorial/wwwroot/css/app.css" id="CssSnippet":::

1. Abra **./Shared/NavMenu.razor** y reemplace su contenido por lo siguiente.

    :::code language="razor" source="../demo/GraphTutorial/Shared/NavMenu.razor" id="NavMenuSnippet":::

1. Abra **./Pages/Index.razor** y reemplace su contenido por lo siguiente.

    :::code language="razor" source="../demo/GraphTutorial/Pages/Index.razor" id="IndexSnippet":::

1. Abra **./Shared/LoginDisplay.razor** y reemplace su contenido por lo siguiente.

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

1. Cree un nuevo directorio en **el directorio ./wwwroot** denominado **img**. Agregue un archivo de imagen de su elección denominado **no-profile-photo.png** en este directorio. Esta imagen se usará como foto del usuario cuando el usuario no tenga ninguna foto en Microsoft Graph.

    > [!TIP]
    > Puede descargar la imagen usada en estas capturas de pantalla desde [GitHub](https://github.com/microsoftgraph/msgraph-training-blazor-clientside/blob/master/demo/GraphTutorial/wwwroot/img/no-profile-photo.png).

1. Guarde todos los cambios y actualice la página.

    ![Una captura de pantalla de la página de inicio rediseñada](./images/create-app-01.png)
