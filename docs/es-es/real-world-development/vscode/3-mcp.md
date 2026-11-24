---
title: "Ejercicio 3 - Probar la funcionalidad con el servidor MCP de Playwright"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Modo agente][previous-lesson] · [Siguiente lección: Agentes personalizados →][next-lesson]

Antes de abrir una solicitud de incorporación de cambios, debes confirmar que la función de filtrado funciona en el navegador. Conectarás el servidor MCP de Playwright y permitirás que Copilot controle un navegador real para probarla.

## Qué es Model Context Protocol (MCP)

MCP permite que los agentes de IA se comuniquen con herramientas externas. Un servidor MCP actúa como puente entre el agente y herramientas como API, paquetes locales o navegadores.

![Diagrama del modo agente y su interacción con contexto, modelos y herramientas de servidores MCP](../../../_images/ex1-mcp-diagram.png)

## Revisa la configuración MCP

El archivo `.vscode/mcp.json` configura los servidores disponibles.

1. Abre `.vscode/mcp.json`.
2. Debe incluir el servidor `github`:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        }
      }
    }
    ```

## Añade el servidor MCP de Playwright

1. Añade una entrada `playwright` junto a `github`:

    ```json
    {
      "servers": {
        "github": {
          "type": "http",
          "url": "https://api.githubcopilot.com/mcp/"
        },
        "playwright": {
          "command": "npx",
          "args": ["@playwright/mcp@latest", "--headless"]
        }
      }
    }
    ```

2. Guarda el archivo.
3. Selecciona **Start** sobre la entrada `playwright` y confirma que confías en el servidor.

## Prueba la función de filtrado

Con el servidor conectado y la aplicación ejecutándose, pide a Copilot:

```text
Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

1. Go to the games page and note how many games are listed.
2. Apply a category filter and confirm the list updates to only show games in that category.
3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
4. Combine a category and a publisher filter and confirm the results respect both.

Report what you observe at each step, and call out anything that does not behave as expected.
```

Si no se encuentra el navegador, pide a Copilot ejecutar:

```bash
npx playwright install chromium
```

## Publica la rama y crea la solicitud

1. Abre el panel **Source Control** y revisa los cambios.
2. Prepáralos seleccionando **+**.
3. Crea un mensaje de confirmación.
4. Selecciona **Publish**.
5. En Copilot Chat, pide que encuentre la incidencia y cree una solicitud de incorporación de cambios para la rama actual.

> [!NOTE]
> Todavía no debes combinar la solicitud.

## Resumen y próximos pasos

Has conectado Playwright MCP, utilizado un navegador real para probar la función y publicado la rama.

A continuación, [crearás un agente personalizado][next-lesson].

## Recursos

- [Introducción a MCP][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Servidor MCP de GitHub][github-mcp-server]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp-server]: https://github.com/github/github-mcp-server
