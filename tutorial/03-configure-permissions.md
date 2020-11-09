---
ms.openlocfilehash: 19bd57df9f349d67e9f10e7dd70f02231950b010
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823423"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework elimina la necesidad de registrar una aplicación en Azure AD para obtener los tokens de acceso para obtener acceso a Microsoft Graph. Controla la autenticación del usuario que ha iniciado sesión en SharePoint, lo que permite al elemento Web obtener tokens de usuario. El elemento web necesita indicar los [ámbitos de permisos de grafos](https://docs.microsoft.com/graph/permissions-reference) que necesita y un administrador de inquilinos que puede aprobar dichos permisos durante la instalación.

## <a name="configure-permissions"></a>Configurar permisos

1. Open **. carpeta/config/package-solution.js**.

1. Agregue el siguiente código a la `solution` propiedad.

    ```json
    "webApiPermissionRequests": [
      {
        "resource": "Microsoft Graph",
        "scope": "Calendars.ReadWrite"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "User.ReadBasic.All"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "Contacts.Read"
      },
      {
        "resource": "Microsoft Graph",
        "scope": "People.Read"
      }
    ]
    ```

El `Calendars.ReadWrite` permiso permite que el elemento Web recupere el calendario del usuario y agregue eventos con Microsoft Graph. Los otros permisos los utilizan los componentes del kit de herramientas de Microsoft Graph para presentar información sobre los asistentes y los organizadores de eventos.

## <a name="optional-test-token-acquisition"></a>Opcional: adquisición de token de prueba

> [!NOTE]
> El resto de los pasos en esta página son opcionales. Si prefiere obtener el código de Microsoft Graph directamente, puede continuar para [obtener una vista de calendario](/graph/tutorials/spfx?tutorial-step=3).

Vamos a agregar código temporal al elemento Web para probar la adquisición de tokens.

1. Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y agregue la siguiente `import` instrucción en la parte superior del archivo.

    ```typescript
    import { AadTokenProvider } from '@microsoft/sp-http';
    ```

1. Reemplace la función `render` existente por lo siguiente.

    ```typescript
    public render(): void {
    this.context.aadTokenProviderFactory
      .getTokenProvider()
      .then((provider: AadTokenProvider)=> {
      provider
        .getToken('https://graph.microsoft.com')
        .then((token: string) => {
          this.domElement.innerHTML = `
          <div class="${ styles.graphTutorial }">
            <div class="${ styles.container }">
              <div class="${ styles.row }">
                <div class="${ styles.column }">
                  <span class="${ styles.title }">Welcome to SharePoint!</span>
                  <p><code style="word-break: break-all;">${ token }</code></p>
                </div>
              </div>
            </div>
          </div>`;
        });
      });
    }
    ```

### <a name="deploy-the-web-part"></a>Implementación del elemento Web

1. Ejecute los dos comandos siguientes en la CLI para crear y empaquetar el elemento Web.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Abra el explorador y vaya al catálogo de aplicaciones de SharePoint del espacio empresarial. Seleccione el elemento de menú **aplicaciones para SharePoint** en el lado izquierdo.

1. Cargue el archivo **./SharePoint/Solution/Graph-tutorial.sppkg** .

1. En el mensaje **¿confía en...** , confirme que el mensaje muestra los 4 permisos de Microsoft Graph que estableció en el **package-solution.jsen** el archivo. Seleccione **hacer que esta solución esté disponible para todos los sitios de la organización** y, después, seleccione **implementar**.

1. Vaya al [centro de administración de SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) con un administrador de inquilinos.

1. En el menú de la izquierda, seleccione **avanzadas** y, a continuación, **acceso a la API**.

1. Seleccione cada una de las solicitudes pendientes del paquete **Graph-tutorial-Client-Side-Solution** y elija **aprobar**.

    ![Captura de pantalla de la página de acceso a la API del centro de administración de SharePoint](images/api-access.png)

### <a name="test-the-web-part"></a>Probar el elemento Web

1. Vaya a un sitio de SharePoint en el que desee probar el elemento Web. Cree una nueva página en la que probar el elemento Web.

1. Use el selector de elementos Web para buscar el elemento Web **GraphTutorial** y agregarlo a la página.

    ![Captura de pantalla del elemento Web GraphTutorial en el selector de elementos Web](images/add-web-part.png)

1. El token de acceso se imprime debajo de la **bienvenida a SharePoint.** mensaje en el elemento Web. Puede copiar este token y analizarlo en [https://jwt.ms/](https://jwt.ms/) para confirmar que contiene los ámbitos de permisos necesarios para el elemento Web.

    ![Captura de pantalla del elemento Web que muestra un token de acceso](images/access-token.png)
