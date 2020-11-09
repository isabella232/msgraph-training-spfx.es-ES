---
ms.openlocfilehash: c239c1ea6daae99cc5a65b7b95508ccb2a1bf014
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823415"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="62c13-101">SharePoint Framework proporciona la [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) para realizar llamadas a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="62c13-101">The SharePoint Framework provides the [MSGraphClient](https://docs.microsoft.com/javascript/api/sp-http/msgraphclient?view=sp-typescript-latest) for making calls to Microsoft Graph.</span></span> <span data-ttu-id="62c13-102">Esta clase ajusta la [biblioteca cliente de JavaScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-sdk-javascript)y la autentica previamente con el usuario que ha iniciado la sesión actual.</span><span class="sxs-lookup"><span data-stu-id="62c13-102">This class wraps the [Microsoft Graph JavaScript Client Library](https://github.com/microsoftgraph/msgraph-sdk-javascript), pre-authenticating it with the current logged on user.</span></span>

<span data-ttu-id="62c13-103">Dado que encapsula la biblioteca de JavaScript existente, su uso es el mismo, y es totalmente compatible con las definiciones de TypeScript de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="62c13-103">Because it wraps the existing JavaScript library, its usage is the same, and it's fully compatible with the Microsoft Graph TypeScript definitions.</span></span>

## <a name="get-the-users-calendar"></a><span data-ttu-id="62c13-104">Obtener el calendario del usuario</span><span class="sxs-lookup"><span data-stu-id="62c13-104">Get the user's calendar</span></span>

1. <span data-ttu-id="62c13-105">Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y agregue las siguientes `import` instrucciones en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="62c13-105">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statements at the top of the file.</span></span>

    ```typescript
    import { MSGraphClient } from '@microsoft/sp-http';
    import * as MicrosoftGraph from '@microsoft/microsoft-graph-types';
    import { startOfWeek, endOfWeek, setDay, set } from 'date-fns';
    ```

1. <span data-ttu-id="62c13-106">Agregue la siguiente función a la clase **GraphTutorialWebPart** para representar un error.</span><span class="sxs-lookup"><span data-stu-id="62c13-106">Add the following function to the **GraphTutorialWebPart** class to render an error.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderGraphErrorSnippet":::

1. <span data-ttu-id="62c13-107">Agregue la siguiente función para imprimir los eventos en el calendario del usuario.</span><span class="sxs-lookup"><span data-stu-id="62c13-107">Add the following function to print out the events in the user's calendar.</span></span>

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

1. <span data-ttu-id="62c13-108">Reemplace la función `render` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="62c13-108">Replace the existing `render` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderSnippet":::

    <span data-ttu-id="62c13-109">Observe lo que hace el código.</span><span class="sxs-lookup"><span data-stu-id="62c13-109">Notice what this code does.</span></span>

    - <span data-ttu-id="62c13-110">Se usa `this.context.msGraphClientFactory.getClient` para obtener un objeto **MSGraphClient** autenticado.</span><span class="sxs-lookup"><span data-stu-id="62c13-110">It uses `this.context.msGraphClientFactory.getClient` to get an authenticated **MSGraphClient** object.</span></span>
    - <span data-ttu-id="62c13-111">Llama al `/me/calendarView` punto de conexión, estableciendo `startDateTime` los `endDateTime` parámetros de consulta y para el inicio y el final de la semana actual.</span><span class="sxs-lookup"><span data-stu-id="62c13-111">It calls the `/me/calendarView` endpoint, setting the `startDateTime` and `endDateTime` query parameters to the start and end of the current week.</span></span>
    - <span data-ttu-id="62c13-112">Usa `select` para limitar los campos que se devuelven, solicitando solo los campos que usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="62c13-112">It uses `select` to limit which fields are returned, requesting only the fields the app uses.</span></span>
    - <span data-ttu-id="62c13-113">Usa `orderby` para ordenar los eventos por su hora de inicio.</span><span class="sxs-lookup"><span data-stu-id="62c13-113">It uses `orderby` to sort the events by their start time.</span></span>
    - <span data-ttu-id="62c13-114">Usa `top` para limitar los resultados a 25 eventos.</span><span class="sxs-lookup"><span data-stu-id="62c13-114">It uses `top` to limit the results to 25 events.</span></span>

## <a name="deploy-the-web-part"></a><span data-ttu-id="62c13-115">Implementación del elemento Web</span><span class="sxs-lookup"><span data-stu-id="62c13-115">Deploy the web part</span></span>

1. <span data-ttu-id="62c13-116">Ejecute los dos comandos siguientes en la CLI para crear y empaquetar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="62c13-116">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="62c13-117">Abra el explorador y vaya al catálogo de aplicaciones de SharePoint del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="62c13-117">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="62c13-118">Seleccione el elemento de menú **aplicaciones para SharePoint** en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="62c13-118">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="62c13-119">Cargue el archivo **./SharePoint/Solution/Graph-tutorial.sppkg** .</span><span class="sxs-lookup"><span data-stu-id="62c13-119">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="62c13-120">En el mensaje **¿confía en...** , confirme que el mensaje muestra los 4 permisos de Microsoft Graph que estableció en el **package-solution.jsen** el archivo.</span><span class="sxs-lookup"><span data-stu-id="62c13-120">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="62c13-121">Seleccione **hacer que esta solución esté disponible para todos los sitios de la organización** y, después, seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="62c13-121">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="62c13-122">Si aún no ha aprobado los permisos de Graph para el elemento Web, hágalo ahora.</span><span class="sxs-lookup"><span data-stu-id="62c13-122">If you have not already approved the Graph permissions for your web part, do that now.</span></span>

    1. <span data-ttu-id="62c13-123">Vaya al [centro de administración de SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) con un administrador de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="62c13-123">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

    1. <span data-ttu-id="62c13-124">En el menú de la izquierda, seleccione **avanzadas** y, a continuación, **acceso a la API**.</span><span class="sxs-lookup"><span data-stu-id="62c13-124">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

    1. <span data-ttu-id="62c13-125">Seleccione cada una de las solicitudes pendientes del paquete **Graph-tutorial-Client-Side-Solution** y elija **aprobar**.</span><span class="sxs-lookup"><span data-stu-id="62c13-125">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

        ![Captura de pantalla de la página de acceso a la API del centro de administración de SharePoint](images/api-access.png)

## <a name="test-the-web-part"></a><span data-ttu-id="62c13-127">Probar el elemento Web</span><span class="sxs-lookup"><span data-stu-id="62c13-127">Test the web part</span></span>

1. <span data-ttu-id="62c13-128">Vaya a un sitio de SharePoint en el que desee probar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="62c13-128">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="62c13-129">Cree una nueva página en la que probar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="62c13-129">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="62c13-130">Use el selector de elementos Web para buscar el elemento Web **GraphTutorial** y agregarlo a la página.</span><span class="sxs-lookup"><span data-stu-id="62c13-130">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Captura de pantalla del elemento Web GraphTutorial en el selector de elementos Web](images/add-web-part.png)

1. <span data-ttu-id="62c13-132">Se imprime una lista de eventos para la semana en curso en el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="62c13-132">A list of events for the current week are printed in the web part.</span></span>

    ![Captura de pantalla del elemento Web que muestra una lista de eventos](images/calendar-list.png)
