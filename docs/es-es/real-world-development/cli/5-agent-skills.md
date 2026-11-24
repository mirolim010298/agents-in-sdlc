---
title: "Lección 5 - Personalizar y utilizar una habilidad quality-checks"
description: "Explora la habilidad existente quality-checks, personaliza el formato del informe y utilízala para validar el filtrado."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Escribir código no es la única parte del trabajo. Ya hemos podido validar manualmente que el código funciona y hemos utilizado archivos de instrucciones para asegurarnos de que sigue nuestras normas. ¿Qué ocurre con las pruebas, lint y el resto de la integración continua (CI)?

Para este tipo de tareas, las **habilidades de agente** son la opción adecuada. Las habilidades ayudan a Copilot a comprender cómo ejecutar correctamente operaciones como estas.

En esta lección:

- explorarás la habilidad existente `quality-checks`;
- personalizarás el formato de sus resultados;
- recargarás y ejecutarás la habilidad.

## Escenario

Tailspin Toys utiliza la habilidad `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos. El equipo quiere mejorar el informe para que los resultados sean más fáciles de leer.

## Instrucciones, scripts y recursos

Las habilidades de agente reúnen instrucciones reutilizables, scripts ejecutables y recursos de apoyo que un agente carga bajo demanda. En esencia, son una carpeta con el nombre de la habilidad y un archivo Markdown llamado `SKILL.md`. El Markdown contiene frontmatter con un nombre y una descripción que indican qué hace la habilidad y cuándo debe llamarse. La carpeta también puede incluir subcarpetas con scripts y otros recursos.

> [!NOTE]
> Una habilidad no necesita carpetas o archivos adicionales. La habilidad `quality-checks` de Tailspin Toys contiene solo `SKILL.md` porque utiliza los comandos existentes del proyecto.

Las habilidades pueden residir en la carpeta `.github/skills` de un proyecto para convertirse en un recurso compartido por el equipo o en la carpeta de habilidades del usuario, `~/.copilot/skills`.

## Explora la habilidad

Vamos a explorar la habilidad creada por el equipo de Tailspin Toys para ejecutar pruebas unitarias, lint y comprobaciones de tipos, llamada `quality-checks`.

1. Vuelve al Codespace y abre `.github/skills/quality-checks/SKILL.md`.
2. Lee los campos `name` y `description` al principio. La descripción ayuda a Copilot a entender cuándo debe llamar a la habilidad.
3. Lee las instrucciones y observa cómo guían a Copilot durante las pruebas y lint.
4. Fíjate en que la habilidad todavía no contiene una sección **Results output formatting**.

## Ejecuta la habilidad antes de hacer cambios

Las habilidades pueden llamarse directamente desde Copilot CLI o mediante lenguaje natural. Pide a Copilot que ejecute las tres comprobaciones.

1. Vuelve a la conversación de filtrado en el modo Interactive.
2. Utiliza el siguiente aviso:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Observa el informe al final.

## Personaliza el informe

Queremos un informe que indique qué se ejecutó, si tuvo éxito y qué comunicaron las herramientas. Vamos a actualizar la habilidad para crear ese informe.

1. Vuelve a `.github/skills/quality-checks/SKILL.md`.
2. Añade la siguiente sección al final del archivo:

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. El archivo se guarda automáticamente.

## Ejecuta la habilidad actualizada

Ahora vemos la actualización en acción. Copilot CLI puede recargar habilidades editadas sin reiniciar la conversación.

1. Introduce:

   ```plaintext
   /skills reload
   ```

2. Utiliza exactamente el mismo aviso de antes:

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. Observa el informe final y compáralo con el primero.

## Resumen y próximos pasos

Has personalizado y utilizado una habilidad existente de agente. En esta lección:

- exploraste la habilidad `quality-checks` para pruebas unitarias, lint y comprobaciones de tipos;
- personalizaste el formato de sus resultados;
- recargaste y ejecutaste la habilidad.

Ese cambio acompañará al filtrado en la PR de la funcionalidad. A continuación, permitirás que Copilot interactúe directamente con el sitio [mediante el servidor MCP de Playwright][next-lesson].

## Más ejemplos de habilidades

Estos ejemplos comunitarios son referencias, no tareas adicionales:

- [Especificación de Agent Skills][skill-spec]
- [Flujo de contribución: `make-repo-contribution`][contribution-example]
- [Documentos de requisitos: `prd`][prd-example]
- [Diagramas y script de exportación incluido: `drawio`][drawio-example]
- [Pruebas de aplicaciones web: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
