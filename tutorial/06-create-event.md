---
ms.openlocfilehash: 0d7c9cc909e2f848cc9760d5862bb1863501f02b
ms.sourcegitcommit: 523e64e972f247e2df57cd8de949ac7bd1b8b047
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/30/2020
ms.locfileid: "48823387"
---
<!-- markdownlint-disable MD002 MD041 -->

En esta sección, actualizará el elemento Web para permitir que el usuario agregue un evento a su calendario para la hora social semanal del equipo. En este escenario, el equipo tiene una hora social semanal a las 4 PM del viernes.

1. Abra **./src/WebParts/graphTutorial/GraphTutorialWebPart.ts** y reemplace el `addSocialToCalendar()` método existente por lo siguiente.

    :::code language="typescript" source="../demo/graph-tutorial/src/webparts/graphTutorial/GraphTutorialWebPart.ts" id="addSocialToCalendarSnippet":::

    Considere lo que hace este código.

    - Determina el próximo viernes siguiente y crea una **fecha** para 4 pm en ese día.
    - Crea un nuevo objeto **MicrosoftGraph. event** , estableciendo el inicio en el valor de la **fecha** y el final de una hora más tarde.
    - Usa **MSGraphClient** para registrar el nuevo evento en el punto de `/me/events` conexión.
    - Vuelve a representar el elemento Web, de modo que la vista se actualiza con el nuevo evento.

1. Cree, empaquete y vuelva a cargar el elemento Web y, a continuación, actualice la página donde lo está probando.

1. Haga clic en el botón **Agregar equipo social** . Una vez actualizada la página, desplácese hacia abajo hasta viernes y busque el nuevo evento.

    ![Captura de pantalla del evento recién creado que se representa en el elemento Web.](images/new-event.png)
