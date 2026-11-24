---
title: "Ejercicio 2 - Añadir funcionalidades con el modo agente de Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Las actualizaciones de una aplicación suelen requerir cambios coordinados en varios archivos y la ejecución de pruebas. El modo agente de Copilot puede explorar el proyecto, realizar las modificaciones necesarias, ejecutar tareas y corregir errores detectados.

En este ejercicio aprenderás a utilizar el modo agente para implementar una nueva función y revisar los cambios y las pruebas antes de incorporarlos.

> [!NOTE]
> El modo agente trabaja dentro del IDE y ofrece ciclos de retroalimentación rápidos. El agente en la nube trabaja de forma asincrónica como un compañero de equipo mediante incidencias y solicitudes de incorporación de cambios.

## Escenario

Tailspin Toys quiere permitir filtrar juegos por categoría y editor. Ya existe una ayuda de editor de datos; ahora completarás la capa de datos, la interfaz y las pruebas.

## Ejecuta el sitio

1. Asegúrate de estar en `main` y actualiza el repositorio.
2. Crea una rama:

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

3. Inicia el sitio:

   ```bash
   npm run dev
   ```

4. Abre `http://localhost:4321` desde el navegador.

## Revisa el backlog

Abre Copilot Chat, selecciona **Agent** y pide ver el backlog del repositorio:

```plaintext
Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
```

## Revisa las instrucciones de interfaz

Abre `.github/instructions/ui.instructions.md` y revisa la arquitectura, los principios de diseño, la accesibilidad y las instrucciones relacionadas con Astro, Tailwind CSS y Drizzle.

## Implementa el filtrado

La funcionalidad requiere:

- Añadir o completar la lógica de filtrado en `src/lib/`.
- Añadir o actualizar las pruebas.
- Actualizar la página de juegos con los controles de filtrado.

1. Abre una conversación nueva o continúa la actual.
2. Selecciona **Add Context**, **Instructions** y el archivo **ui**.
3. Selecciona **Agent** y envía:

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

4. Revisa los cambios propuestos y confirma que las pruebas pasen.
5. Acepta los cambios mediante **Keep**.
6. Verifica la nueva funcionalidad en el navegador.

> [!CAUTION]
> Revisa siempre el código generado por Copilot o cualquier otra herramienta de IA.

## Resumen y próximos pasos

Has utilizado el modo agente para implementar una nueva funcionalidad en varias partes del proyecto y revisar las pruebas antes de incorporarla.

A continuación, [probarás la función con el servidor MCP de Playwright][next-lesson].

## Recursos

- [Modos Ask, Edit y Agent][choose-mode]
- [Modo agente en VS Code][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
