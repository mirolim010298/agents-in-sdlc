---
title: "Lección 7 - Crear y utilizar un agente de control de calidad"
description: "Crea un agente personalizado de control de calidad que combine los requisitos de la incidencia, la habilidad quality-checks y Playwright MCP."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Has utilizado la habilidad `quality-checks` para ejecutar comprobaciones automatizadas y Playwright MCP para observar la experiencia de filtrado en un navegador. Ahora reunirás esas capacidades en un agente personalizado con un proceso de control de calidad claramente definido.

En esta lección:

- explorarás cómo un agente personalizado funciona con instrucciones, habilidades y herramientas MCP;
- crearás e inspeccionarás un perfil reutilizable de control de calidad;
- seleccionarás el agente de control de calidad y revisarás sus resultados frente a la incidencia de filtrado.

## Escenario

Tailspin Toys quiere revisar de forma coherente los requisitos, la calidad del código, las comprobaciones automatizadas, la cobertura de las pruebas y el comportamiento en el navegador antes de abrir una solicitud de incorporación de cambios (PR). Un agente personalizado puede coordinar ese proceso y proporcionar un informe reutilizable.

## Qué es un agente personalizado

Un agente personalizado es una versión especializada de Copilot definida en un perfil Markdown. El perfil describe el propósito del agente, sus instrucciones y las herramientas disponibles. En este taller, definirás una función de control de calidad en `.github/agents/qa.agent.md` y la seleccionarás en Copilot CLI.

Las personalizaciones utilizadas tienen funciones diferentes. Las instrucciones del repositorio describen las normas del equipo. La habilidad `quality-checks` agrupa comprobaciones repetibles. Playwright MCP proporciona herramientas de navegador. El perfil de control de calidad indica a Copilot cómo utilizar estas capacidades para evaluar los requisitos e informar de los resultados. No las sustituye ni requiere otra conversación.

## Crea el perfil de control de calidad

Antes de abrir la PR de la funcionalidad, pedirás a Copilot que cree un perfil reutilizable de control de calidad. El perfil definirá las comprobaciones que realiza y los límites que debe respetar.

1. Vuelve a tu Codespace y confirma que la conversación de filtrado está en el modo Interactive.
2. Pide al agente predeterminado que cree el nuevo agente personalizado:

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## Inspecciona el perfil

Antes de utilizar el nuevo agente, revisa su perfil para confirmar que Copilot ha registrado el flujo de trabajo y los límites previstos. Así evitarás que un agente incompleto o demasiado amplio modifique la funcionalidad cuando solo quieres que se verifique.

1. Introduce `/diff` y abre `.github/agents/qa.agent.md`.
2. Lee el frontmatter. El campo `description` es obligatorio; `name` es opcional, aunque incluirlo proporciona al agente un nombre visible claro.
3. Lee las instrucciones del perfil y confirma que el control de calidad empieza por los requisitos, sigue las instrucciones del repositorio, ejecuta la habilidad `quality-checks` y utiliza Playwright MCP.
4. Confirma que informa con pruebas de respaldo, pide permiso antes de cambiar código de implementación y no confirma cambios ni abre solicitudes de incorporación de cambios.
5. Si el perfil generado omite alguna responsabilidad o límite, pide al agente predeterminado que lo revise antes de continuar.

## Ejecuta el control de calidad frente a la incidencia

Copilot CLI carga los agentes del proyecto al comenzar una conversación. Reanuda la misma conversación de filtrado después de crear el perfil y selecciona el agente de control de calidad para que pueda utilizar la incidencia y las decisiones de planificación que ya están en el contexto.

1. Activa el agente con el siguiente mensaje:

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> Como acabas de crear el agente, puede que no aparezca en la lista de agentes disponibles. Está disponible y el comando anterior lo activará.

2. Utiliza el siguiente mensaje para pedir al agente de control de calidad que revise la funcionalidad:

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. ¡El agente de control de calidad se pondrá manos a la obra!
4. Cuando termine, lee el informe que proporcione.

## Resumen y próximos pasos

Has añadido al flujo de trabajo una función especializada reutilizable y revisado su trabajo. En esta lección:

- exploraste cómo un agente personalizado funciona con instrucciones, habilidades y herramientas MCP;
- creaste e inspeccionaste un perfil reutilizable de control de calidad;
- seleccionaste el agente de control de calidad y revisaste sus resultados frente a la incidencia de filtrado.

Ahora tienes lista la implementación, la actualización de la habilidad, el perfil de control de calidad, las pruebas y el informe de verificación. A continuación, [los reunirás en una PR de funcionalidad y utilizarás Agent Merge][next-lesson].

## Recursos

- [Crear agentes personalizados para Copilot CLI][create-agents]
- [Configuración de agentes personalizados][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
