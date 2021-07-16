---
ms.openlocfilehash: 25caea9275c57faa9c741e274ac90606959422c2
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446987"
---
<!-- markdownlint-disable MD002 MD041 -->

En este tutorial se enseña a crear una aplicación de Blazor WebAssembly del lado cliente que use la API de Microsoft Graph para recuperar información de calendario para un usuario.

> [!TIP]
> Si prefiere descargar el tutorial completado, puede descargar o clonar el [repositorio GitHub archivo](https://github.com/microsoftgraph/msgraph-training-blazor-clientside). Consulta el archivo README en la carpeta **de demostración** para obtener instrucciones sobre cómo configurar la aplicación con un identificador de aplicación y un secreto.

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, debe tener [instalado el SDK de .NET Core](https://dotnet.microsoft.com/download) en el equipo de desarrollo. Si no tiene el SDK, visite el vínculo anterior para ver las opciones de descarga.

También debe tener una cuenta personal de Microsoft con un buzón en Outlook.com, o una cuenta de Trabajo o escuela de Microsoft. Si no tienes una cuenta de Microsoft, hay un par de opciones para obtener una cuenta gratuita:

- Puede registrarse [para obtener una nueva cuenta personal de Microsoft](https://signup.live.com/signup?wa=wsignin1.0&rpsnv=12&ct=1454618383&rver=6.4.6456.0&wp=MBI_SSL_SHARED&wreply=https://mail.live.com/default.aspx&id=64855&cbcxt=mai&bk=1454618383&uiflavor=web&uaid=b213a65b4fdc484382b6622b3ecaa547&mkt=E-US&lc=1033&lic=1).
- Puedes [registrarte en el programa Office 365 desarrolladores](https://developer.microsoft.com/office/dev-program) para obtener una suscripción Office 365 gratuita.

> [!NOTE]
> Este tutorial se escribió con .NET Core SDK versión 5.0.302. Los pasos de esta guía pueden funcionar con otras versiones, pero eso no se ha probado.

## <a name="feedback"></a>Comentarios

Proporcione cualquier comentario sobre este tutorial en el [repositorio GitHub archivo](https://github.com/microsoftgraph/msgraph-training-blazor-clientside).
