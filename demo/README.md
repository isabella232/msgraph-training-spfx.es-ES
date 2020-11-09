---
ms.openlocfilehash: ca72a0d6047d3cd275d34e2d0b4e3c54dbab5375
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48831351"
---
# <a name="how-to-run-the-completed-project"></a>Cómo ejecutar el proyecto completado

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar el proyecto completado en esta carpeta, necesita lo siguiente:

- [Node.js](https://nodejs.org/en/download/releases/) versión 10. x
- [Gulp](https://gulpjs.com/)
- Una cuenta profesional o educativa de Microsoft, con acceso a una cuenta de administrador global de la misma organización. Si no tiene una cuenta de Microsoft, puede [suscribirse al programa de desarrolladores de office 365](https://developer.microsoft.com/office/dev-program) para obtener una suscripción gratuita a Office 365.
- Su inquilino de Microsoft 365 debe estar [configurado para el desarrollo de SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/set-up-your-developer-tenant), con un catálogo de aplicaciones y un sitio de prueba creados antes de iniciar este tutorial.

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

    ![Captura de pantalla de la página de acceso a la API del centro de administración de SharePoint](../tutorial/images/api-access.png)

### <a name="test-the-web-part"></a>Probar el elemento Web

1. Vaya a un sitio de SharePoint en el que desee probar el elemento Web. Cree una nueva página en la que probar el elemento Web.

1. Use el selector de elementos Web para buscar el elemento Web **GraphTutorial** y agregarlo a la página.

    ![Captura de pantalla del elemento Web GraphTutorial en el selector de elementos Web](../tutorial/images/add-web-part.png)
