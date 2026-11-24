---
title: "Lección 6 - Validar la funcionalidad con Playwright MCP"
description: "Inspecciona o configura Playwright MCP en Copilot CLI y utilízalo para explorar la función de filtrado en un navegador."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Como ya hemos destacado, escribir código no es la única parte del trabajo. Tenemos que trabajar con datos, servicios externos y permitir a Copilot que utilice automatizaciones adicionales. Aquí es donde entran en juego los servidores MCP. Permiten a Copilot ir más allá de las funciones integradas en CLI y proporcionarle más herramientas y servicios.

En esta lección:

- comprenderás qué es Model Context Protocol (MCP) y cómo lo utiliza Copilot CLI;
- añadirás el servidor MCP de Playwright si todavía no está disponible;
- pedirás al agente que controle un navegador y explore la función de filtrado.

## Escenario

Aunque las pruebas unitarias y de extremo a extremo son importantes, validar cambios en la interfaz exige interactuar con ella. Quieres permitir que Copilot utilice el sitio web como lo haría una persona usuaria para automatizar aún más los cambios y aumentar la confianza en que los resultados se comportan como se espera.

## Qué es Model Context Protocol (MCP)

[Model Context Protocol (MCP)][mcp-blog-post] proporciona a los agentes de IA una forma de comunicarse con herramientas y servicios externos. Mediante MCP, pueden comunicarse con herramientas y servicios externos en tiempo real. Esto les permite acceder a información actualizada y realizar acciones en tu nombre.

Estas herramientas y recursos se acceden mediante un servidor MCP, que actúa como puente entre el agente de IA y las herramientas y servicios externos. Cada servidor MCP representa un conjunto distinto de herramientas y recursos a los que el agente puede acceder.

Dos servidores MCP populares son:

- **[Servidor MCP de GitHub][github-mcp]**: proporciona acceso a API para gestionar repositorios, incidencias y solicitudes de incorporación de cambios de GitHub.
- **[Servidor MCP de Playwright][playwright-mcp-server]**: proporciona capacidades de automatización de navegador mediante Playwright.

Hay muchos otros servidores MCP disponibles. GitHub mantiene un [registro MCP][mcp-registry] para facilitar su descubrimiento y contribución.

> [!CAUTION]
> Trata los servidores MCP como cualquier otra dependencia del proyecto. Antes de utilizar uno, revisa su código fuente, verifica el editor y considera las implicaciones de seguridad.

## Añade el servidor MCP de Playwright

Si el servidor MCP de Playwright todavía no está disponible, añádelo para que Copilot pueda interactuar con el sitio web como lo haría una persona usuaria.

> [!NOTE]
> Si Playwright MCP ya está configurado en Copilot CLI, omite estos pasos de configuración y continúa con la siguiente sección.

1. Vuelve al Codespace.
2. Abre el diálogo para añadir un servidor MCP introduciendo el siguiente comando en Copilot CLI:

   ```plaintext
   /mcp add
   ```

3. Como nombre, introduce `playwright` y pulsa <kbd>Tab</kbd>.
4. Confirma el tipo de servidor **STDIO** pulsando <kbd>Enter</kbd> y, después, pulsa <kbd>Tab</kbd>.
5. Pega lo siguiente en el diálogo **Command**:

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

6. Pulsa <kbd>Control</kbd>+<kbd>S</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) para guardar el nuevo servidor MCP.
7. Pulsa <kbd>Esc</kbd> para salir del diálogo MCP.

## Pide a Copilot que explore la funcionalidad mediante Playwright

Antes comprobaste manualmente que la funcionalidad se comportaba como se esperaba. Ahora, utilizaremos el servidor MCP de Playwright disponible en Copilot para hacer lo mismo.

1. Utiliza el siguiente mensaje para indicar a Copilot que use Playwright MCP y valide la funcionalidad:

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

> [!NOTE]
> No es necesario indicar a Copilot que utilice el servidor MCP, porque normalmente lo descubrirá por sí mismo. Sin embargo, como ya sabes qué debe utilizar, orientarle no suele ser una mala idea: ayuda a obtener resultados más consistentes y ahorra algunos tokens.

2. Observa cómo Copilot enumera los distintos pasos que realiza en el navegador para confirmar que la funcionalidad funciona.
3. Lee el informe y confirma que todo se comporta como se espera.

Copilot iniciará el servidor, utilizará Playwright para interactuar con el sitio web, detendrá el servidor y te ofrecerá un informe.

## Resumen y próximos pasos

¡Enhorabuena! Has utilizado el servidor MCP de Playwright para explorar la funcionalidad en un navegador real desde Copilot CLI. En resumen:

- aprendiste qué es Model Context Protocol (MCP) y cómo lo utiliza Copilot CLI;
- añadiste el servidor MCP de Playwright si no estaba disponible;
- pediste al agente que controlara un navegador y explorara la funcionalidad de filtrado.

A continuación, [crearás un agente personalizado de control de calidad][next-lesson] que reúna la habilidad y las herramientas del navegador en una función especializada.

## Recursos

- [Qué es MCP y por qué se habla tanto de él][mcp-blog-post]
- [Servidor MCP de Microsoft Playwright][playwright-mcp-server]
- [Añadir servidores MCP a Copilot CLI][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
