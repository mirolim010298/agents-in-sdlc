---
title: "Lección 9 - Comandos de barra en GitHub Copilot CLI"
description: "Explora comandos de barra para gestionar el contexto, seleccionar modelos, compartir sesiones y delegar opcionalmente a la nube."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como cualquier herramienta CLI bien diseñada, GitHub Copilot CLI incluye numerosos comandos de barra para interactuar con ella. Estos comandos exponen funciones avanzadas, información interna y opciones de configuración adicionales. Ya has utilizado comandos como `/diff`, `/mcp`, `/skills`, `/agent` y `/pr`. Ahora vamos a explorar algunos más.

En esta lección:

- utilizarás `/context` y `/compact` para explorar cómo Copilot gestiona el contexto de la conversación;
- utilizarás `/model` para explorar los modelos disponibles;
- aprenderás cómo `/share` puede exportar o compartir una sesión;
- explorarás comandos opcionales para trabajo paralelo, árboles de trabajo y delegación al agente en la nube.

## Escenario

Ya has completado el flujo principal de CLI. Ahora veremos algunas funciones adicionales: gestión del contexto, cambio de modelos, uso compartido de sesiones y delegación opcional al [agente de GitHub Copilot en la nube][about-cloud-agent].

## Explora el contexto de Copilot CLI

Al trabajar en tareas grandes o complejas, puedes alcanzar el límite de la ventana de contexto del modelo. Copilot CLI compacta automáticamente la conversación cuando hace falta, y puedes inspeccionarla o compactarla con comandos de barra.

1. Vuelve al Codespace e inicia Copilot CLI desde la raíz del repositorio si aún no está abierto.
2. Introduce:

   ```plaintext
   /context
   ```

3. Observa el modelo, el uso actual de tokens y cómo se divide el contexto entre instrucciones del sistema, herramientas, mensajes y espacio libre.
4. Compacta la conversación:

   ```plaintext
   /compact
   ```

5. Introduce `/context` de nuevo y compara el resultado. Puede que no haya cambios drásticos si la conversación ya era pequeña.

> [!NOTE]
> Copilot CLI compacta automáticamente el contexto a medida que se llena la ventana. Utiliza `/compact` si quieres elegir el momento. Usa `/clear` o `/new` al cambiar a una tarea no relacionada y quieras empezar una conversación nueva.

## Elige tu modelo

Los modelos tienen diferentes puntos fuertes y las personas desarrolladoras tienen preferencias distintas. Copilot CLI permite listar y seleccionar el modelo que quieres utilizar.

1. Introduce:

   ```plaintext
   /model
   ```

2. Explora los modelos disponibles y la información de uso.
3. Conserva el modelo actual, selecciona otro o pulsa <kbd>Esc</kbd> para cerrar la lista.

## Comparte una sesión

Trabajar en equipo y compartir los aprendizajes ayuda a todas las personas a mejorar su uso de las herramientas de IA. El comando `/share` puede exportar una sesión a un archivo Markdown o HTML, crear un enlace compartible o publicar un gist de GitHub.

1. Introduce `/help` y revisa las opciones de `/share` disponibles en tu versión instalada.
2. Si quieres compartir esta sesión, elige el destino que se ajuste a tus necesidades, por ejemplo `/share file` para una exportación local a Markdown.
3. Revisa el contenido exportado antes de enviarlo a alguien o publicarlo. Las exportaciones pueden incluir mensajes, respuestas y detalles del proyecto.

Publicar un enlace o gist es opcional. No publiques contenido del repositorio o de la conversación que tu equipo no haya acordado compartir.

## Opcional: amplía el trabajo o delega

El taller principal ya está completo. Copilot CLI también proporciona comandos para tareas mayores:

- `/fleet` puede dividir subtareas independientes entre subagentes y ejecutarlas en paralelo.
- `/worktree` puede crear un árbol de trabajo de Git aislado para una tarea independiente.
- `/delegate` puede enviar una tarea al agente de GitHub Copilot en la nube, que trabaja de forma asincrónica y puede abrir una solicitud de incorporación de cambios.

Estos comandos son opcionales porque pueden crear árboles de trabajo o trabajo remoto adicionales. Antes de probarlos, empieza una tarea nueva con un alcance claro y revisa el resultado con el flujo de trabajo habitual. Si quieres profundizar en el trabajo asincrónico con agentes, continúa con el [taller del agente en la nube][cloud-workshop].

## Resumen y próximos pasos

Los comandos de barra de Copilot CLI permiten configurarlo, compartir sesiones y consultar qué ocurre entre bastidores. En esta lección:

- utilizaste `/context` y `/compact` para explorar cómo Copilot gestiona el contexto;
- utilizaste `/model` para explorar los modelos disponibles;
- aprendiste cómo `/share` puede exportar o compartir una sesión;
- exploraste comandos opcionales para trabajo paralelo, árboles de trabajo y delegación al agente en la nube.

¡Hay más comandos de barra disponibles y más posibilidades por explorar con Copilot CLI! Cerremos el recorrido [revisando lo aprendido][next-lesson] y qué puedes hacer después.

## Recursos

- [Referencia de comandos de Copilot CLI][cli-reference]
- [Gestión del contexto en Copilot CLI][context-management]
- [Acerca del agente de GitHub Copilot en la nube][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
