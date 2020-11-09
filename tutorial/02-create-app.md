---
ms.openlocfilehash: 5164c68a78837c179636f685d28ddf61f93f8415
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823400"
---
<!-- markdownlint-disable MD002 MD041 -->

En este tutorial, creará un [elemento Web del lado cliente de SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/overview-client-side-web-parts) que usará Microsoft Graph para obtener el calendario del usuario para la semana actual y permitir que el usuario agregue un evento a su calendario.

## <a name="create-a-web-part-project"></a>Crear un proyecto de elementos Web

1. Abra la interfaz de línea de comandos (CLI) en un directorio vacío donde desee crear el proyecto. Ejecute el siguiente comando para iniciar el generador de SharePoint de Yeoman.

    ```Shell
    yo @microsoft/sharepoint
    ```

1. Responda a los mensajes como se indica a continuación.

    - **¿Cuál es el nombre de la solución?** `graph-tutorial`
    - **¿Qué paquetes de línea de base desea que se destinen al componente o los componentes?** `SharePoint Online only (latest)`
    - **¿Dónde desea ubicar los archivos?** `Use the current folder`
    - **¿Desea permitir que el administrador de inquilinos pueda implementar la solución en todos los sitios inmediatamente sin ejecutar ninguna implementación de características ni agregar aplicaciones en sitios?** `Yes`
    - **¿Los componentes de la solución requieren permisos para obtener acceso a las API Web que son únicas y no se comparten con otros componentes de la diez ANT?** `No`
    - **¿Cuál es el tipo de componente del lado cliente que se va a crear?** `WebPart`
    - **¿Cómo se llama su elemento web?** `GraphTutorial`
    - **¿Cuál es la descripción del elemento web?** `GraphTutorial description`
    - **¿Qué marco desea utilizar?** `No JavaScript framework`

1. Ejecute el siguiente comando para actualizar la versión de TypeScript del proyecto a 3,7.

    ```Shell
    npm install @microsoft/rush-stack-compiler-3.7 --save-dev
    ```

1. Abra **./tsconfig.jsen** y reemplace `rush-stack-compiler-3.3` por `rush-stack-compiler-3.7` .

1. Abra **./tslint.jsen** y quite la `"no-use-before-declare": true,` línea. La `no-use-before-declare` regla está en desuso y se producirá un error durante el proceso de compilación.

## <a name="install-dependencies"></a>Instalar dependencias

Antes de continuar, instale algunos paquetes NPM adicionales que usará más adelante.

- [Definiciones de TypeScript de Microsoft Graph](https://github.com/microsoftgraph/msgraph-typescript-typings) para proporcionar IntelliSense para los objetos de Microsoft Graph.
- [Kit de herramientas de Microsoft Graph](https://docs.microsoft.com/graph/toolkit/overview) para proporcionar componentes de interfaz de usuario para el elemento Web.
- [Date-FNS](https://date-fns.org/) para obtener funciones útiles para trabajar con fechas.

```Shell
npm install @microsoft/microsoft-graph-types@1.17.0 --save-dev
npm install @microsoft/mgt@1.3.4 date-fns @2.16.0
```
