---
ms.openlocfilehash: bb55b2bea2497628ceb2e09c889ce62e773d8e71
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823407"
---
<!-- markdownlint-disable MD002 MD041 -->

Este tutorial le enseña a crear un [elemento Web del lado cliente de SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) que use la API de Microsoft Graph para recuperar la información de calendario de un usuario.

> [!TIP]
> Si prefiere descargar solo el tutorial completo, puede descargar o clonar el repositorio de [GitHub](https://github.com/microsoftgraph/msgraph-training-spfx).

## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar este tutorial, debe tener las siguientes herramientas instaladas en el equipo de desarrollo.

- [Node.js](https://nodejs.org/en/download/releases/)
- [Yeoman](https://yeoman.io/)
- [Gulp](https://gulpjs.com/)
- [Generador de SharePoint de Yeoman](https://docs.microsoft.com/sharepoint/dev/spfx/toolchain/scaffolding-projects-using-yeoman-sharepoint-generator)

Puede encontrar más información sobre los requisitos para el desarrollo de SharePoint Framework en [configurar el entorno de desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-development-environment).

> [!IMPORTANT]
> SharePoint Framework requiere Node.js versión 10. x. Asegúrese de instalar la versión correcta.

También debe tener una cuenta profesional o educativa de Microsoft, con acceso a una cuenta de administrador global de la misma organización. Si no tiene una cuenta de Microsoft, puede [suscribirse al programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.

Su inquilino de Microsoft 365 debe estar [configurado para el desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), con un catálogo de aplicaciones y un sitio de prueba creados antes de iniciar este tutorial.

> [!NOTE]
> Este tutorial se ha redactado con las siguientes versiones de las herramientas anteriores. Los pasos de esta guía pueden funcionar con otras versiones, pero no se han probado.
>
> - Node.js 10.22.0
> - Yeoman 3.1.1
> - Gulp 4.0.2
> - Herramienta del generador de SharePoint de Yeoman 1.11.0

## <a name="feedback"></a>Comentarios

Envíe sus comentarios sobre este tutorial en el [repositorio de github](https://github.com/microsoftgraph/msgraph-training-spfx).
