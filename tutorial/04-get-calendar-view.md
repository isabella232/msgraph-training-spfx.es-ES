---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823415"
---
<!-- markdownlint-disable MD002 MD041 -->

SharePoint Framework proporciona la [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) para realizar llamadas a Microsoft Graph. Esta clase ajusta la [biblioteca cliente de JavaScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)y la autentica previamente con el usuario que ha iniciado la sesión actual.

Dado que encapsula la biblioteca de JavaScript existente, su uso es el mismo, y es totalmente compatible con las definiciones de TypeScript de Microsoft Graph.

## <a name="get-the-users-calendar"></a>Obtener el calendario del usuario

1. Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y agregue las siguientes `import` instrucciones en la parte superior del archivo.

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. Agregue la siguiente función a la clase **GraphTutorialWebPart** para representar un error.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. Agregue la siguiente función para imprimir los eventos en el calendario del usuario.

    ```typescript
    private renderCalendarView(events: MicrosoftGraph.Event[]) : void {
      const viewContainer = this.domElement.querySelector('#calendarView');
      let html = '';

      // Temporary: print events as a list
      for(const event of events) {
        html += `
          <p class="${ styles.description }">Subject: ${event.subject}</p>
          <p class="${ styles.description }">Organizer: ${event.organizer.emailAddress.name}</p>
          <p class="${ styles.description }">Start: ${event.start.dateTime}</p>
          <p class="${ styles.description }">End: ${event.end.dateTime}</p>
          `;
      }

      viewContainer.innerHTML = html;
    }
    ```

1. Reemplace la función `render` existente por lo siguiente.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    Observe lo que hace el código.

    - Se usa `this.context.msGraphClientFactory.getClient` para obtener un objeto **MSGraphClient** autenticado.
    - Llama al `/me/calendarView` punto de conexión, estableciendo `startDateTime` los `endDateTime` parámetros de consulta y para el inicio y el final de la semana actual.
    - Usa `select` para limitar los campos que se devuelven, solicitando solo los campos que usa la aplicación.
    - Usa `orderby` para ordenar los eventos por su hora de inicio.
    - Usa `top` para limitar los resultados a 25 eventos.

## <a name="deploy-the-web-part"></a>Implementación del elemento Web

1. Ejecute los dos comandos siguientes en la CLI para crear y empaquetar el elemento Web.

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. Abra el explorador y vaya al catálogo de aplicaciones de SharePoint del espacio empresarial. Seleccione el elemento de menú **aplicaciones para SharePoint** en el lado izquierdo.

1. Cargue el archivo **./SharePoint/Solution/Graph-tutorial.sppkg** .

1. En el mensaje **¿confía en...** , confirme que el mensaje muestra los 4 permisos de Microsoft Graph que estableció en el **package-solution.jsen** el archivo. Seleccione **hacer que esta solución esté disponible para todos los sitios de la organización** y, después, seleccione **implementar**.

1. Si aún no ha aprobado los permisos de Graph para el elemento Web, hágalo ahora.

    1. Vaya al [centro de administración de SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) con un administrador de inquilinos.

    1. En el menú de la izquierda, seleccione **avanzadas** y, a continuación, **acceso a la API**.

    1. Seleccione cada una de las solicitudes pendientes del paquete **Graph-tutorial-Client-Side-Solution** y elija **aprobar**.

        ![Captura de pantalla de la página de acceso a la API del centro de administración de SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a>Probar el elemento Web

1. Vaya a un sitio de SharePoint en el que desee probar el elemento Web. Cree una nueva página en la que probar el elemento Web.

1. Use el selector de elementos Web para buscar el elemento Web **GraphTutorial** y agregarlo a la página.

    ![Captura de pantalla del elemento Web GraphTutorial en el selector de elementos Web](images/add-web-part.png)

1. Se imprime una lista de eventos para la semana en curso en el elemento Web.

    ![Captura de pantalla del elemento Web que muestra una lista de eventos](images/calendar-list.png)
