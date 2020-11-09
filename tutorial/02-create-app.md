---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823400"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="23e3e-101">En este tutorial, creará un [elemento Web del lado cliente de SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) que usará Microsoft Graph para obtener el calendario del usuario para la semana actual y permitir que el usuario agregue un evento a su calendario.</span><span class="sxs-lookup"><span data-stu-id="23e3e-101">In this tutorial, you'll create a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that will use Microsoft Graph to get the user's calendar for the current week and allow the user to add an event to their calendar.</span></span>

## <a name="create-a-web-part-project"></a><span data-ttu-id="23e3e-102">Crear un proyecto de elementos Web</span><span class="sxs-lookup"><span data-stu-id="23e3e-102">Create a web part project</span></span>

1. <span data-ttu-id="23e3e-103">Abra la interfaz de línea de comandos (CLI) en un directorio vacío donde desee crear el proyecto.</span><span class="sxs-lookup"><span data-stu-id="23e3e-103">Open your command-line interface (CLI) in an empty directory where you want to create the project.</span></span> <span data-ttu-id="23e3e-104">Ejecute el siguiente comando para iniciar el generador de SharePoint de Yeoman.</span><span class="sxs-lookup"><span data-stu-id="23e3e-104">Run the following command to start the Yeoman SharePoint generator.</span></span>

    ```Shell
    yo @microsoft/sharepoint
    ```

1. <span data-ttu-id="23e3e-105">Responda a los mensajes como se indica a continuación.</span><span class="sxs-lookup"><span data-stu-id="23e3e-105">Respond to the prompts as follows.</span></span>

    - <span data-ttu-id="23e3e-106">**¿Cuál es el nombre de la solución?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-106">**What is your solution name?**</span></span> `graph-tutorial`
    - <span data-ttu-id="23e3e-107">**¿Qué paquetes de línea de base desea que se destinen al componente o los componentes?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-107">**Which baseline packages do you want to target for your component(s)?**</span></span> `SharePoint Online only (latest)`
    - <span data-ttu-id="23e3e-108">**¿Dónde desea ubicar los archivos?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-108">**Where do you want to place the files?**</span></span> `Use the current folder`
    - <span data-ttu-id="23e3e-109">**¿Desea permitir que el administrador de inquilinos pueda implementar la solución en todos los sitios inmediatamente sin ejecutar ninguna implementación de características ni agregar aplicaciones en sitios?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-109">**Do you want to allow the tenant admin the choice of being able to deploy the solution to all sites immediately without running any feature deployment or adding apps in sites?**</span></span> `Yes`
    - <span data-ttu-id="23e3e-110">**¿Los componentes de la solución requieren permisos para obtener acceso a las API Web que son únicas y no se comparten con otros componentes de la diez ANT?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-110">**Will the components in the solution require permissions to access web APIs that are unique and not shared with other components in the ten ant?**</span></span> `No`
    - <span data-ttu-id="23e3e-111">**¿Cuál es el tipo de componente del lado cliente que se va a crear?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-111">**Which type of client-side component to create?**</span></span> `WebPart`
    - <span data-ttu-id="23e3e-112">**¿Cómo se llama su elemento web?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-112">**What is your Web part name?**</span></span> `GraphTutorial`
    - <span data-ttu-id="23e3e-113">**¿Cuál es la descripción del elemento web?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-113">**What is your Web part description?**</span></span> `GraphTutorial description`
    - <span data-ttu-id="23e3e-114">**¿Qué marco desea utilizar?**</span><span class="sxs-lookup"><span data-stu-id="23e3e-114">**Which framework would you like to use?**</span></span> `No JavaScript framework`

1. <span data-ttu-id="23e3e-115">Ejecute el siguiente comando para actualizar la versión de TypeScript del proyecto a 3,7.</span><span class="sxs-lookup"><span data-stu-id="23e3e-115">Run the following command to update the TypeScript version in the project to 3.7.</span></span>

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. <span data-ttu-id="23e3e-116">Abra **./tsconfig.jsen** y reemplace `rush-stack-compiler-3.3` por `rush-stack-compiler-3.7` .</span><span class="sxs-lookup"><span data-stu-id="23e3e-116">Open **./tsconfig.json** and replace `rush-stack-compiler-3.3` with `rush-stack-compiler-3.7`.</span></span>

1. <span data-ttu-id="23e3e-117">Abra **./tslint.jsen** y quite la `"no-use-before-declare": true,` línea.</span><span class="sxs-lookup"><span data-stu-id="23e3e-117">Open **./tslint.json** and remove the `"no-use-before-declare": true,` line.</span></span> <span data-ttu-id="23e3e-118">La `no-use-before-declare` regla está en desuso y se producirá un error durante el proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="23e3e-118">The `no-use-before-declare` rule is deprecated and will cause an error during the build process.</span></span>

## <a name="install-dependencies"></a><span data-ttu-id="23e3e-119">Instalar dependencias</span><span class="sxs-lookup"><span data-stu-id="23e3e-119">Install dependencies</span></span>

<span data-ttu-id="23e3e-120">Antes de continuar, instale algunos paquetes NPM adicionales que usará más adelante.</span><span class="sxs-lookup"><span data-stu-id="23e3e-120">Before moving on, install some additional NPM packages that you will use later.</span></span>

- <span data-ttu-id="23e3e-121">[Definiciones de TypeScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) para proporcionar IntelliSense para los objetos de Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="23e3e-121">[Microsoft Graph TypeScript definitions](https://github.com/microsoftgraph/msgraph-typescript-typings) to provide Intellisense for Microsoft Graph objects.</span></span>
- <span data-ttu-id="23e3e-122">[Kit de herramientas de Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) para proporcionar componentes de interfaz de usuario para el elemento Web.</span><span class="sxs-lookup"><span data-stu-id="23e3e-122">[Microsoft Graph Toolkit](https://docs.microsoft.com/graph/toolkit/overview) to provide UI components for the web part.</span></span>
- <span data-ttu-id="23e3e-123">[Date-FNS](https://date-fns.org/) para obtener funciones útiles para trabajar con fechas.</span><span class="sxs-lookup"><span data-stu-id="23e3e-123">[date-fns](https://date-fns.org/) for helpful functions for working with dates.</span></span>

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
