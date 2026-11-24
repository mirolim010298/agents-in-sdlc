---
title: "Ejercicio 4 - Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

En los ejercicios anteriores pediste al agente de GitHub Copilot en la nube que asumiera varias tareas destinadas a mejorar la experiencia de usuario y añadir funcionalidades. Aunque el agente está diseñado para funcionar de forma asincrónica y autónoma, sigue siendo importante supervisar esas tareas.

Puedes utilizar la [página de agentes][agents-page] de GitHub.com. Desde este centro de control podrás ver todas las tareas de agentes que tienen solicitudes de incorporación de cambios abiertas, explorar las operaciones realizadas e incluso dirigir una sesión en curso.

## Revisa las tareas del agente

1. Navega hasta la [página de agentes de Copilot](https://github.com/copilot/agents).
2. Observa la lista de tareas, incluidas las asignadas a Copilot:
   - Actualización de la documentación.
   - Generación de API para modificar juegos.
   - Añadir un modo de alto contraste al sitio.
3. Selecciona una tarea en curso y revisa las operaciones que Copilot ha realizado.
4. En el panel derecho podrás ver la solicitud de incorporación de cambios y los archivos modificados.

> [!NOTE]
> Los pasos exactos varían según el estado del trabajo y el enfoque que haya elegido Copilot.

## Dirige el agente en la nube

Pide a Copilot que añada también un modo claro mientras trabaja en el modo de alto contraste.

1. Selecciona la sesión relacionada con el modo de alto contraste.

    ![Sesión de accesibilidad en el centro de control](../../../_images/ex6-accessibility-session.png)

2. Espera a que indique que ha terminado la configuración y ha empezado a trabajar.
3. En el diálogo **Steer active session while Copilot is working**, añade la siguiente instrucción:

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Captura de pantalla de la tarea del agente en la nube con el diálogo de dirección resaltado](../../../_images/ex6-steer-cloud-agent-task.png)

4. Pulsa <kbd>Enter</kbd> para enviar la instrucción.
5. Observa cómo Copilot reconoce la instrucción y la incorpora a su flujo de trabajo.

## Deja que Copilot haga su trabajo

El agente aplicará la nueva solicitud después de finalizar el paso que estaba realizando. La ejecución puede tardar varios minutos.

## Resumen y próximos pasos

Has utilizado el panel de agentes como centro de control para supervisar y orientar tareas del agente en la nube.

A continuación, [iterarás sobre las solicitudes de incorporación de cambios que haya creado Copilot][next-lesson].

## Recursos

- [Página de agentes de Copilot][agents-page]
- [Acerca de los agentes personalizados][custom-agents]

---

| [← Lección anterior: Agentes personalizados][previous-lesson] | [Siguiente lección: Iterar sobre el trabajo de Copilot →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
