---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823407"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="49141-101">Este tutorial le enseña a crear un [elemento Web del lado cliente de SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) que use la API de Microsoft Graph para recuperar la información de calendario de un usuario.</span><span class="sxs-lookup"><span data-stu-id="49141-101">This tutorial teaches you how to build a [SharePoint client-side web part](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) that uses the Microsoft Graph API to retrieve calendar information for a user.</span></span>

> [!TIP]
> <span data-ttu-id="49141-102">Si prefiere descargar solo el tutorial completo, puede descargar o clonar el repositorio de [GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="49141-102">If you prefer to just download the completed tutorial, you can download or clone the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49141-103">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="49141-103">Prerequisites</span></span>

<span data-ttu-id="49141-104">Antes de iniciar este tutorial, debe tener las siguientes herramientas instaladas en el equipo de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="49141-104">Before you start this tutorial, you should have the following tools installed on your development machine.</span></span>

- [<span data-ttu-id="49141-105">Node.js</span><span class="sxs-lookup"><span data-stu-id="49141-105">Node.js</span></span>](https://nodejs.org/en/download/releases/)
- [<span data-ttu-id="49141-106">Yeoman</span><span class="sxs-lookup"><span data-stu-id="49141-106">Yeoman</span></span>](https://yeoman.io/)
- [<span data-ttu-id="49141-107">Gulp</span><span class="sxs-lookup"><span data-stu-id="49141-107">Gulp</span></span>](https://gulpjs.com/)
- [<span data-ttu-id="49141-108">Generador de SharePoint de Yeoman</span><span class="sxs-lookup"><span data-stu-id="49141-108">Yeoman SharePoint generator</span></span>](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

<span data-ttu-id="49141-109">Puede encontrar más información sobre los requisitos para el desarrollo de SharePoint Framework en [configurar el entorno de desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span><span class="sxs-lookup"><span data-stu-id="49141-109">You can find more details about requirements for SharePoint Framework development at [Set up your SharePoint Framework development environment](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49141-110">SharePoint Framework requiere Node.js versión 10. x.</span><span class="sxs-lookup"><span data-stu-id="49141-110">SharePoint Framework requires Node.js version 10.x.</span></span> <span data-ttu-id="49141-111">Asegúrese de instalar la versión correcta.</span><span class="sxs-lookup"><span data-stu-id="49141-111">Be sure to install the correct version.</span></span>

<span data-ttu-id="49141-112">También debe tener una cuenta profesional o educativa de Microsoft, con acceso a una cuenta de administrador global de la misma organización.</span><span class="sxs-lookup"><span data-stu-id="49141-112">You should also have a Microsoft work or school account, with access to a global administrator account in the same organization.</span></span> <span data-ttu-id="49141-113">Si no tiene una cuenta de Microsoft, puede [suscribirse al programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.</span><span class="sxs-lookup"><span data-stu-id="49141-113">If you don't have a Microsoft account, you can [sign up for the Office 365 Developer Program](https://developer.microsoft.com/office/dev-program) to get a free Office 365 subscription.</span></span>

<span data-ttu-id="49141-114">Su inquilino de Microsoft 365 debe estar [configurado para el desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), con un catálogo de aplicaciones y un sitio de prueba creados antes de iniciar este tutorial.</span><span class="sxs-lookup"><span data-stu-id="49141-114">Your Microsoft 365 tenant should be [setup for SharePoint Framework development](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), with an app catalog and testing site created before you start this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="49141-115">Este tutorial se ha redactado con las siguientes versiones de las herramientas anteriores.</span><span class="sxs-lookup"><span data-stu-id="49141-115">This tutorial was written with the following versions of the above tools.</span></span> <span data-ttu-id="49141-116">Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.</span><span class="sxs-lookup"><span data-stu-id="49141-116">The steps in this guide may work with other versions, but that has not been tested.</span></span>
>
> - <span data-ttu-id="49141-117">Node.js 10.22.0</span><span class="sxs-lookup"><span data-stu-id="49141-117">Node.js 10.22.0</span></span>
> - <span data-ttu-id="49141-118">Yeoman 3.1.1</span><span class="sxs-lookup"><span data-stu-id="49141-118">Yeoman 3.1.1</span></span>
> - <span data-ttu-id="49141-119">Gulp 4.0.2</span><span class="sxs-lookup"><span data-stu-id="49141-119">Gulp 4.0.2</span></span>
> - <span data-ttu-id="49141-120">Herramienta del generador de SharePoint de Yeoman 1.11.0</span><span class="sxs-lookup"><span data-stu-id="49141-120">Yeoman SharePoint generator 1.11.0</span></span>

## <a name="feedback"></a><span data-ttu-id="49141-121">Comentarios</span><span class="sxs-lookup"><span data-stu-id="49141-121">Feedback</span></span>

<span data-ttu-id="49141-122">Envíe sus comentarios sobre este tutorial en el [repositorio de github](https://github.com/microsoftgraph/msgraph-training-spfx).</span><span class="sxs-lookup"><span data-stu-id="49141-122">Please provide any feedback on this tutorial in the [GitHub repository](https://github.com/microsoftgraph/msgraph-training-spfx).</span></span>
