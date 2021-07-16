---
ms.openlocfilehash: c9fb7269969b0ef4e0300b8884c3ed168216b6cc
ms.sourcegitcommit: ef990e983274cb161bfe16a8dff801d30a798f04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2021
ms.locfileid: "53446969"
---
<!-- markdownlint-disable MD002 MD041 -->

En este ejercicio, creará un nuevo registro de aplicaciones web de Azure AD mediante el Centro Azure Active Directory administración.

1. Abra un explorador y vaya al [centro de administración de Azure Active Directory](https://aad.portal.azure.com). Inicie sesión con una **cuenta personal** (también conocida como: cuenta Microsoft) o una **cuenta profesional o educativa**.

1. Seleccione **Azure Active Directory** en el panel de navegación izquierdo y, a continuación, seleccione **Registros de aplicaciones** en **Administrar**.

    ![Captura de pantalla de los registros de la aplicación ](./images/aad-portal-app-registrations.png)

1. Seleccione **Nuevo registro**. En la página **Registrar una aplicación**, establezca los valores siguientes.

    - Establezca **Nombre** como `Blazor Graph Tutorial`.
    - Establezca **Tipos de cuenta admitidos** en **Cuentas en cualquier directorio de organización y cuentas personales de Microsoft**.
    - En **URI de** redireccionamiento, establezca la primera lista desplegable en Aplicación de página única **(SPA)** y establezca el valor en `https://localhost:5001/authentication/login-callback` .

    ![Captura de pantalla de la página Registrar una aplicación](./images/aad-register-an-app.png)

1. Seleccione **Registrar**. En la página Graph tutorial de **Blazor,** copie el valor del identificador de aplicación **(cliente)** y guárdelo, lo necesitará en el paso siguiente.

    ![Una captura de pantalla del Id. de aplicación del nuevo registro de la aplicación](./images/aad-application-id.png)
