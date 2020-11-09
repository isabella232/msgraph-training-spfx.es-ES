---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823387"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="86be6-101">En esta sección, actualizará el elemento Web para permitir que el usuario agregue un evento a su calendario para la hora social semanal del equipo.</span><span class="sxs-lookup"><span data-stu-id="86be6-101">In this section you'll update the web part to allow the user to add an event to their calendar for the team's weekly social hour.</span></span> <span data-ttu-id="86be6-102">En este escenario, el equipo tiene una hora social semanal a las 4 PM del viernes.</span><span class="sxs-lookup"><span data-stu-id="86be6-102">In this scenario, the team has a weekly social hour at 4 PM on Friday.</span></span>

1. <span data-ttu-id="86be6-103">Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y reemplace el `addSocialToCalendar()` método existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="86be6-103">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and replace the existing `addSocialToCalendar()` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    <span data-ttu-id="86be6-104">Considere lo que hace este código.</span><span class="sxs-lookup"><span data-stu-id="86be6-104">Consider what this code does.</span></span>

    - <span data-ttu-id="86be6-105">Determina el próximo viernes siguiente y crea una **fecha** para 4 pm en ese día.</span><span class="sxs-lookup"><span data-stu-id="86be6-105">It determines the next upcoming Friday and constructs a **Date** for 4 PM on that day.</span></span>
    - <span data-ttu-id="86be6-106">Crea un nuevo objeto **MicrosoftGraph. event** , estableciendo el inicio en el valor de la **fecha** y el final de una hora más tarde.</span><span class="sxs-lookup"><span data-stu-id="86be6-106">It constructs a new **MicrosoftGraph.Event** object, setting the start to the value of the **Date** , and the end for one hour later.</span></span>
    - <span data-ttu-id="86be6-107">Usa **MSGraphClient** para registrar el nuevo evento en el punto de `/me/events` conexión.</span><span class="sxs-lookup"><span data-stu-id="86be6-107">It uses the **MSGraphClient** to POST the new event to the `/me/events` endpoint.</span></span>
    - <span data-ttu-id="86be6-108">Vuelve a representar el elemento Web, de modo que la vista se actualiza con el nuevo evento.</span><span class="sxs-lookup"><span data-stu-id="86be6-108">It re-renders the web part so the view is updated with the new event.</span></span>

1. <span data-ttu-id="86be6-109">Cree, empaquete y vuelva a cargar el elemento Web y, a continuación, actualice la página donde lo está probando.</span><span class="sxs-lookup"><span data-stu-id="86be6-109">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

1. <span data-ttu-id="86be6-110">Haga clic en el botón **Agregar equipo social** .</span><span class="sxs-lookup"><span data-stu-id="86be6-110">Click the **Add team social** button.</span></span> <span data-ttu-id="86be6-111">Una vez actualizada la página, desplácese hacia abajo hasta viernes y busque el nuevo evento.</span><span class="sxs-lookup"><span data-stu-id="86be6-111">Once the page refreshes, scroll down to Friday and find the new event.</span></span>

    ![Captura de pantalla del evento recién creado que se representa en el elemento Web.](images/new-event.png)
