---
title: "Ejercicio 5: Iteración sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

## Revisar el trabajo

A lo largo de este laboratorio has trabajado con GitHub Copilot en varias tareas destinadas a mejorar la experiencia de usuario y añadir funcionalidades: documentación, una función de juegos relacionados y funciones de accesibilidad. Revisa los cambios y proporciona comentarios a Copilot cuando sea necesario.

## Seguridad y agente en la nube

Como el agente en la nube trabaja de forma asincrónica y sin supervisión directa, existen ciertas restricciones:

- Copilot tiene acceso de lectura al repositorio y acceso de escritura únicamente a la rama que utiliza para el código.
- El agente se ejecuta dentro de GitHub Actions en un entorno separado y efímero.
- Los flujos de trabajo de GitHub Actions requieren la aprobación de una persona.
- [El acceso a recursos externos está limitado por defecto][agent-firewall], incluidos los servidores MCP.

## Revisa la documentación generada

1. Abre la solicitud de incorporación de cambios creada por Copilot, por ejemplo una titulada **Add missing documentation**.
2. Selecciona **Files changed** y revisa los comentarios TSDoc y la documentación generada.
3. Si todo parece correcto, vuelve a **Conversation** y aprueba los flujos de trabajo que estén esperando aprobación mediante **Approve and run workflows**.

> [!NOTE]
> Es posible que veas una advertencia porque Copilot está bloqueado por el cortafuegos. Es normal: el agente tiene acceso limitado a recursos externos.

## Solicita cambios

Puedes comentar en la solicitud de incorporación de cambios o hacer comentarios en línea. Copilot iniciará una nueva sesión para atenderlos.

Ejemplos de solicitudes:

- Añadir encabezados de comentarios al principio de cada archivo.
- Añadir comentarios TSDoc a archivos de TypeScript y Astro.
- Crear un README con una descripción de la estructura de la aplicación Astro.

También puedes utilizar `@copilot` en un comentario. Cuando termines, convierte la solicitud de borrador a lista para revisión y combínala.

## Revisa la función de juegos relacionados

Abre la solicitud titulada de forma similar a **Show related games on the game details page** y revisa los cambios generados:

1. Confirma que se añadió una ayuda de acceso a datos.
2. Comprueba la sección de juegos relacionados.
3. Verifica que se maneje el caso sin juegos relacionados.
4. Revisa las pruebas unitarias.

Si quieres probar manualmente el cambio, cambia a la rama creada por Copilot en un codespace y ejecuta:

```bash
git fetch origin
git checkout <branch-name>
```

## Revisa las funciones de accesibilidad

Revisa la solicitud relacionada con el modo de alto contraste. Comprueba:

- Los componentes de la interfaz para cambiar de modo.
- El uso de almacenamiento local.
- Los cambios de CSS para los modos de alto contraste y claro.
- Los atributos de accesibilidad y la navegación mediante teclado.
- El código que gestiona el cambio de modo.

## Ejercicio opcional: sigue delegando

El agente en la nube funciona bien con tareas reales del backlog. Algunos ejemplos son:

- Crear un formulario de interés de mecenas.
- Implementar paginación en la lista de juegos.
- Añadir validación de entrada y gestión de errores.

## Resumen

Has completado el recorrido del agente en la nube:

- Revisaste los archivos de instrucciones.
- Asignaste incidencias al agente.
- Supervisaste y dirigiste sesiones.
- Revisaste solicitudes de incorporación de cambios e iteraste sobre ellas.

## Revisión y próximos pasos

Los otros recorridos complementan lo que has practicado:

- 🖥️ **[Recorrido de VS Code](../../vscode/)**: utiliza el modo agente de Copilot Chat y MCP.
- 💻 **[Recorrido de CLI](../../cli/)**: realiza cambios revisados desde la terminal.

## Recursos

- [GitHub Copilot][github-copilot]
- [Acerca de los agentes de Copilot][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas del agente en la nube][cloud-agent-best-practices]
- [Configurar el cortafuegos del agente en la nube][agent-firewall]

---

| [← Lección anterior: Gestión de agentes][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall

[previous-lesson]: ../4-managing-agents/
