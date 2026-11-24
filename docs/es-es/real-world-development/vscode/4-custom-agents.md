---
title: "Ejercicio 4 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## Qué son los agentes personalizados

Los [agentes personalizados][custom-agents-concept] permiten crear asistentes de IA especializados para tareas o ámbitos concretos. Se definen mediante archivos Markdown en `.github/agents` y proporcionan a Copilot instrucciones específicas, buenas prácticas y conocimientos del dominio.

Los agentes personalizados tienen su propia ventana de contexto y pueden orquestar habilidades y otros agentes.

> [!NOTE]
> No hay una única forma correcta de crear un agente personalizado. Prueba y itera hasta encontrar el enfoque adecuado.

## Escenario

Tailspin Toys quiere mejorar la accesibilidad de su plataforma. El diseño actual presenta un contraste insuficiente para algunas personas. El equipo solicita un modo de alto contraste que pueda activarse y desactivarse.

## Revisa el agente de accesibilidad

1. Abre `.github/agents/accessibility.md`.
2. Observa los campos `name` y `description` del frontmatter.
3. Revisa las responsabilidades principales, las buenas prácticas y los ejemplos de código.

> [!CAUTION]
> Los campos `name` y `description` son obligatorios.

## Utiliza el agente en Copilot Chat

1. Crea una rama nueva:

   ```bash
   git checkout main
   git pull
   git checkout -b accessibility-vscode
   ```

2. Abre Copilot Chat y selecciona **Accessibility agent** en el selector de agentes.
3. Envía:

   ```plaintext
   Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
   ```

4. Revisa las modificaciones propuestas y las pruebas que genere el agente.

## Resumen y próximos pasos

Has utilizado un agente personalizado para implantar una funcionalidad de accesibilidad.

En el siguiente ejercicio, [supervisarás y dirigirás el trabajo del agente][next-lesson].

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
