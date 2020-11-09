---
ms.openlocfilehash: ee9addcbcf58fa971b3e67fb3d84cfb36bf275dd
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823427"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="b77f8-101">En esta sección, usará el kit de [herramientas de Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) para reemplazar la lista simple de eventos con una interfaz de usuario enriquecida.</span><span class="sxs-lookup"><span data-stu-id="b77f8-101">In this section, you'll use the [Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to replace the simple list of events with rich UI.</span></span>

<span data-ttu-id="b77f8-102">El kit de herramientas proporciona un [componente de agenda](https://docs.microsoft.com/graph/toolkit/components/agenda), que está bien adaptado para representar nuestra lista de eventos.</span><span class="sxs-lookup"><span data-stu-id="b77f8-102">The toolkit provides an [Agenda component](https://docs.microsoft.com/graph/toolkit/components/agenda), which is well-suited to render our list of events.</span></span>

## <a name="update-the-web-part"></a><span data-ttu-id="b77f8-103">Actualizar el elemento Web</span><span class="sxs-lookup"><span data-stu-id="b77f8-103">Update the web part</span></span>

1. <span data-ttu-id="b77f8-104">Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.Module.SCSS**.</span><span class="sxs-lookup"><span data-stu-id="b77f8-104">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.module.scss**.</span></span> <span data-ttu-id="b77f8-105">Cambie el valor del `background-color` atributo de la `.row` entrada a `$ms-color-white` .</span><span class="sxs-lookup"><span data-stu-id="b77f8-105">Change the value of the `background-color` attribute in the `.row` entry to `$ms-color-white`.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="rowScssSnippet" highlight="4":::

1. <span data-ttu-id="b77f8-106">Agregue la siguiente entrada dentro de la `.graphTutorial` entrada.</span><span class="sxs-lookup"><span data-stu-id="b77f8-106">Add the following entry inside the `.graphTutorial` entry.</span></span>

    :::code language="css" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.module.scss" id="addSocialBtnSnippet":::

1. <span data-ttu-id="b77f8-107">Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y agregue la siguiente `import` instrucción en la parte superior del archivo.</span><span class="sxs-lookup"><span data-stu-id="b77f8-107">Open **./src/webparts/graphTutorial/GraphTutorialWebPart.ts** and add the following `import` statement at the top of the file.</span></span>

    ```typescript
    import { Providers, SharePointProvider, MgtAgenda } from '@microsoft/mgt';
    ```

1. <span data-ttu-id="b77f8-108">Agregue la siguiente función a la clase **GraphTutorialWebPart** para inicializar el kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="b77f8-108">Add the following function to the **GraphTutorialWebPart** class to initialize the toolkit.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="onInitSnippet":::

1. <span data-ttu-id="b77f8-109">Reemplace la función `renderCalendarView` existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b77f8-109">Replace the existing `renderCalendarView` function with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="renderCalendarViewSnippet":::

    <span data-ttu-id="b77f8-110">Esto reemplaza la lista básica con el componente de **agenda** del kit de herramientas.</span><span class="sxs-lookup"><span data-stu-id="b77f8-110">This replaces the basic list with the **Agenda** component from the toolkit.</span></span>

1. <span data-ttu-id="b77f8-111">Cree, empaquete y vuelva a cargar el elemento Web y, a continuación, actualice la página donde lo está probando.</span><span class="sxs-lookup"><span data-stu-id="b77f8-111">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span>

    ![Captura de pantalla del elemento Web con el componente de agenda](images/mgt-agenda.png)

## <a name="an-alternate-approach"></a><span data-ttu-id="b77f8-113">Un método alternativo</span><span class="sxs-lookup"><span data-stu-id="b77f8-113">An alternate approach</span></span>

<span data-ttu-id="b77f8-114">En este punto, tiene código que:</span><span class="sxs-lookup"><span data-stu-id="b77f8-114">At this point, you have code that:</span></span>

- <span data-ttu-id="b77f8-115">Usa el **MSGraphClient** para obtener la vista de calendario del usuario de la semana actual de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b77f8-115">Uses the **MSGraphClient** to get the user's calendar view for the current week from Microsoft Graph.</span></span>
- <span data-ttu-id="b77f8-116">Agregue estos eventos al componente **agenda** desde el kit de herramientas de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b77f8-116">Add those events to the **Agenda** component from the Microsoft Graph Toolkit.</span></span>

<span data-ttu-id="b77f8-117">Con este enfoque, tiene control total sobre la llamada a la API de Graph y puede realizar cualquier procesamiento de los eventos antes de la representación que desee.</span><span class="sxs-lookup"><span data-stu-id="b77f8-117">With this approach, you have full control over the Graph API call and can do any processing of the events prior to rendering that you want.</span></span> <span data-ttu-id="b77f8-118">Sin embargo, si no es necesario, puede simplificar la tarea, ya que el componente de **agenda** hará el trabajo por usted.</span><span class="sxs-lookup"><span data-stu-id="b77f8-118">However, if that isn't required, you can simplify by letting the **Agenda** component do the work for you.</span></span>

<span data-ttu-id="b77f8-119">Todos los componentes del kit de herramientas de Microsoft Graph pueden realizar todas las llamadas de API relevantes a Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="b77f8-119">All Microsoft Graph Toolkit components are capable of making all of the relevant API calls to the Microsoft Graph.</span></span> <span data-ttu-id="b77f8-120">Por ejemplo, agregando el componente de **agenda** al elemento Web y no estableciendo ninguna propiedad, el elemento Web usaría la configuración predeterminada para obtener eventos para el día actual.</span><span class="sxs-lookup"><span data-stu-id="b77f8-120">For example, by just adding the **Agenda** component to the web part, and not setting any properties, the web part would use its default settings to get events for the current day.</span></span> <span data-ttu-id="b77f8-121">Veamos cómo podemos lograr los mismos resultados que actualmente tiene (eventos para la semana actual).</span><span class="sxs-lookup"><span data-stu-id="b77f8-121">Let's look at how we can achieve the same results we currently have (events for the current week).</span></span>

1. <span data-ttu-id="b77f8-122">Reemplace el `render` método existente por lo siguiente.</span><span class="sxs-lookup"><span data-stu-id="b77f8-122">Replace the existing `render` method with the following.</span></span>

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="alternateRenderSnippet":::

    <span data-ttu-id="b77f8-123">Ahora, en lugar de realizar una llamada de API `render` , simplemente se agrega un `mgt-agenda` elemento directamente en el HTML.</span><span class="sxs-lookup"><span data-stu-id="b77f8-123">Now, instead of making an API call in `render`, you simply add an `mgt-agenda` element directly into the HTML.</span></span> <span data-ttu-id="b77f8-124">Al establecer el `date` Inicio de la semana y `days` a 7, el componente hará la misma llamada a la API que la versión anterior de `render` .</span><span class="sxs-lookup"><span data-stu-id="b77f8-124">By setting `date` to the start of the week, and `days` to 7, the component will make the same API call the previous version of `render` was making.</span></span>

1. <span data-ttu-id="b77f8-125">Agregue la siguiente función vacía a la clase **GraphTutorialWebPart** .</span><span class="sxs-lookup"><span data-stu-id="b77f8-125">Add the following empty function to the **GraphTutorialWebPart** class.</span></span>

    ```typescript
    private async addSocialToCalendar() {}
    ```

    > [!NOTE]
    > <span data-ttu-id="b77f8-126">También se ha agregado un botón **Agregar equipo social** al elemento Web y se ha agregado el `addSocialToCalendar` método como un agente de escucha de eventos.</span><span class="sxs-lookup"><span data-stu-id="b77f8-126">We also added an **Add team social** button to the web part, and added the `addSocialToCalendar` method as an event listener.</span></span>  <span data-ttu-id="b77f8-127">Implementará el código que se encuentra en la siguiente sección.</span><span class="sxs-lookup"><span data-stu-id="b77f8-127">You'll implement the code behind that in the next section.</span></span> <span data-ttu-id="b77f8-128">Por ahora, solo queremos que el código se compile.</span><span class="sxs-lookup"><span data-stu-id="b77f8-128">For now, we just want the code to compile.</span></span>

1. <span data-ttu-id="b77f8-129">Cree, empaquete y vuelva a cargar el elemento Web y, a continuación, actualice la página donde lo está probando.</span><span class="sxs-lookup"><span data-stu-id="b77f8-129">Build, package, and re-upload the web part, then refresh the page where you are testing it.</span></span> <span data-ttu-id="b77f8-130">La vista debe ser la misma que la prueba anterior.</span><span class="sxs-lookup"><span data-stu-id="b77f8-130">The view should be the same as your previous test.</span></span>

### <a name="using-the-toolkit-vs-making-api-calls"></a><span data-ttu-id="b77f8-131">Usar el kit de herramientas y realizar llamadas API</span><span class="sxs-lookup"><span data-stu-id="b77f8-131">Using the toolkit vs making API calls</span></span>

<span data-ttu-id="b77f8-132">En este momento, es posible que se pregunte por el problema de usar el **MSGraphClient** en absoluto, cuando el kit de herramientas realice el trabajo por usted.</span><span class="sxs-lookup"><span data-stu-id="b77f8-132">At this point you may be wondering why you went through the trouble of using the **MSGraphClient** at all, when the toolkit does the work for you.</span></span> <span data-ttu-id="b77f8-133">El kit de herramientas está diseñado para representar los resultados que se consultan en Microsoft Graph, como una lista de eventos.</span><span class="sxs-lookup"><span data-stu-id="b77f8-133">The toolkit is designed for rendering results that you query from Microsoft Graph, such as a list of events.</span></span> <span data-ttu-id="b77f8-134">Sin embargo, hay escenarios en los que es necesario realizar llamadas a la API.</span><span class="sxs-lookup"><span data-stu-id="b77f8-134">However, there are scenarios where making API calls yourself is necessary.</span></span>

- <span data-ttu-id="b77f8-135">Cualquier llamada a la API que no sea una `GET` solicitud.</span><span class="sxs-lookup"><span data-stu-id="b77f8-135">Any API calls that are not a `GET` request.</span></span> <span data-ttu-id="b77f8-136">Por ejemplo, la creación de un nuevo evento en el calendario o la actualización del número de teléfono de un usuario.</span><span class="sxs-lookup"><span data-stu-id="b77f8-136">For example, creating a new event on the calendar, or updating a user's phone number.</span></span>
- <span data-ttu-id="b77f8-137">Llamadas a la API para obtener datos destinados a ser usados "en segundo plano" y no representados directamente.</span><span class="sxs-lookup"><span data-stu-id="b77f8-137">API calls to get data that's intended to be used "behind the scenes" and not rendered directly.</span></span>
