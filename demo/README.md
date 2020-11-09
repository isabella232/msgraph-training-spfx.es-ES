---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831351"
---
# <a name="how-to-run-the-completed-project"></a><span data-ttu-id="94cf5-101">Cómo ejecutar el proyecto completado</span><span class="sxs-lookup"><span data-stu-id="94cf5-101">How to run the completed project</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94cf5-102">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="94cf5-102">Prerequisites</span></span>

<span data-ttu-id="94cf5-103">Para ejecutar el proyecto completado en esta carpeta, necesita lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="94cf5-103">To run the completed project in this folder, you need the following:</span></span>

- <span data-ttu-id="94cf5-104">[Node.js](https://nodejs.org/en/download/releases/) versión 10. x</span><span class="sxs-lookup"><span data-stu-id="94cf5-104">[Node.js](https://nodejs.org/en/download/releases/) version 10.x</span></span>
- [<span data-ttu-id="94cf5-105">Gulp</span><span class="sxs-lookup"><span data-stu-id="94cf5-105">Gulp</span></span>](https://gulpjs.com/)
- <span data-ttu-id="94cf5-106">Una cuenta profesional o educativa de Microsoft, con acceso a una cuenta de administrador global de la misma organización.</span><span class="sxs-lookup"><span data-stu-id="94cf5-106">A Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="94cf5-107">Si no tiene una cuenta de Microsoft, puede [suscribirse al programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.</span><span class="sxs-lookup"><span data-stu-id="94cf5-107">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>
- <span data-ttu-id="94cf5-108">Su inquilino de Microsoft 365 debe estar [configurado para el desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), con un catálogo de aplicaciones y un sitio de prueba creados antes de iniciar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="94cf5-108">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

### <a name="deploy-the-web-part"></a><span data-ttu-id="94cf5-109">Implementación del elemento Web</span><span class="sxs-lookup"><span data-stu-id="94cf5-109">Deploy the web part</span></span>

1. <span data-ttu-id="94cf5-110">Ejecute los dos comandos siguientes en la CLI para crear y empaquetar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="94cf5-110">Run the following two commands in your CLI to build and package your web part.</span></span>

    ```Shell
    gulp bundle --ship
    gulp package-solution --ship
    ```

1. <span data-ttu-id="94cf5-111">Abra el explorador y vaya al catálogo de aplicaciones de SharePoint del espacio empresarial.</span><span class="sxs-lookup"><span data-stu-id="94cf5-111">Open your browser and go to your tenant's SharePoint App Catalog.</span></span> <span data-ttu-id="94cf5-112">Seleccione el elemento de menú **aplicaciones para SharePoint** en el lado izquierdo.</span><span class="sxs-lookup"><span data-stu-id="94cf5-112">Select the **Apps for SharePoint** menu item on the left-hand side.</span></span>

1. <span data-ttu-id="94cf5-113">Cargue el archivo **./SharePoint/Solution/Graph-tutorial.sppkg** .</span><span class="sxs-lookup"><span data-stu-id="94cf5-113">Upload the **./sharepoint/solution/graph-tutorial.sppkg** file.</span></span>

1. <span data-ttu-id="94cf5-114">En el mensaje **¿confía en...** , confirme que el mensaje muestra los 4 permisos de Microsoft Graph que estableció en el **package-solution.jsen** el archivo.</span><span class="sxs-lookup"><span data-stu-id="94cf5-114">In the **Do you trust...** prompt, confirm that the prompt lists the 4 Microsoft Graph permissions you set in the **package-solution.json** file.</span></span> <span data-ttu-id="94cf5-115">Seleccione **hacer que esta solución esté disponible para todos los sitios de la organización** y, después, seleccione **implementar**.</span><span class="sxs-lookup"><span data-stu-id="94cf5-115">Select **Make this solution available to all sites in the organization** , then select **Deploy**.</span></span>

1. <span data-ttu-id="94cf5-116">Vaya al [centro de administración de SharePoint](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) con un administrador de inquilinos.</span><span class="sxs-lookup"><span data-stu-id="94cf5-116">Go to the [SharePoint admin center](https://admin.microsoft.com/sharepoint?page=classicfeatures&modern=true) using a tenant administrator.</span></span>

1. <span data-ttu-id="94cf5-117">En el menú de la izquierda, seleccione **avanzadas** y, a continuación, **acceso a la API**.</span><span class="sxs-lookup"><span data-stu-id="94cf5-117">In the left-hand menu, select **Advanced** , then **API access**.</span></span>

1. <span data-ttu-id="94cf5-118">Seleccione cada una de las solicitudes pendientes del paquete **Graph-tutorial-Client-Side-Solution** y elija **aprobar**.</span><span class="sxs-lookup"><span data-stu-id="94cf5-118">Select each of the pending requests from the **graph-tutorial-client-side-solution** package and choose **Approve**.</span></span>

    ![Captura de pantalla de la página de acceso a la API del centro de administración de SharePoint](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a><span data-ttu-id="94cf5-120">Probar el elemento Web</span><span class="sxs-lookup"><span data-stu-id="94cf5-120">Test the web part</span></span>

1. <span data-ttu-id="94cf5-121">Vaya a un sitio de SharePoint en el que desee probar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="94cf5-121">Go to a SharePoint site where you want to test the web part.</span></span> <span data-ttu-id="94cf5-122">Cree una nueva página en la que probar el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="94cf5-122">Create a new page to test the web part on.</span></span>

1. <span data-ttu-id="94cf5-123">Use el selector de elementos Web para buscar el elemento Web **GraphTutorial** y agregarlo a la página.</span><span class="sxs-lookup"><span data-stu-id="94cf5-123">Use the web part picker to find the **GraphTutorial** web part and add it to the page.</span></span>

    ![Captura de pantalla del elemento Web GraphTutorial en el selector de elementos Web](../tutorial/images/add-web-part.png)
