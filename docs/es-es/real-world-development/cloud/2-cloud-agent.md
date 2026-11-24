---
title: "Ejercicio 2 - Agente de GitHub Copilot en la nube"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Instrucciones personalizadas][previous-lesson] |
|:--|

Pocas organizaciones, si alguna, no tienen dificultades con la deuda técnica. Puede tratarse de problemas de seguridad sin resolver, código heredado que requiere actualizaciones o solicitudes de funciones que llevan tiempo pendientes por falta de tiempo. El agente de GitHub Copilot en la nube puede realizar tareas como actualizar código y añadir funcionalidades de forma autónoma. Al finalizar su trabajo, genera una solicitud de incorporación de cambios en borrador lista para que la revise un desarrollador. Así se pueden delegar tareas tediosas y acelerar el desarrollo para que el equipo se centre en elementos de mayor importancia.

Explorarás los siguientes aspectos con el agente de GitHub Copilot en la nube:

- Personalizar el entorno utilizado para generar código.
- Garantizar que las operaciones se realicen de forma segura.
- Comprender la importancia de definir bien el alcance de las incidencias.
- Asignar incidencias a Copilot.

## Escenarios

Tailspin Toys quiere resolver parte de su deuda técnica. Los contratistas que crearon la primera versión del sitio dejaron la documentación en un estado poco adecuado, por no decir que prácticamente no existe. Como primer paso, quieren que se añadan comentarios TSDoc a todas las funciones exportadas de la aplicación.

Además, el equipo de diseño quiere mejorar el descubrimiento de juegos. Solicita que la página de detalles de cada juego muestre juegos relacionados, es decir, otros títulos de la misma categoría, para que las personas puedan seguir navegando. No necesitan una implementación pulida todavía; solo quieren algo que puedan utilizar para las pruebas de aceptación de la experiencia de usuario. Esta tarea está bloqueada en este momento, aunque hay otras incidencias con mayor prioridad.

Estos son ejemplos de tareas que pueden quedar aplazadas, por lo que son buenas candidatas para asignarlas al agente de GitHub Copilot en la nube. El agente podrá trabajar de forma asincrónica y permitir que el desarrollador se ocupe de otras tareas, para volver más tarde y revisar su trabajo y confirmar que todo es correcto.

## Presentación del agente de GitHub Copilot en la nube

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) puede realizar tareas en segundo plano, de forma parecida a como lo haría una persona desarrolladora. También permite varias formas de trabajar, por ejemplo, [asignar una incidencia de GitHub a Copilot](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions). Al asignarla, Copilot crea una solicitud de incorporación de cambios en borrador, prepara un entorno y comienza a trabajar en la tarea. Puedes revisar su sesión mientras está en curso o después de finalizarla.

## La importancia de las instrucciones con un alcance claro

GitHub Copilot no elimina la necesidad de pensar. Incluso las operaciones aparentemente sencillas ganan complejidad cuando se analiza su contexto. [Define con cuidado el alcance de las tareas para el agente en la nube][cloud-agent-best-practices]. Trátalo como a un compañero de programación con IA: trabaja por etapas, aprende, experimenta y adapta el enfoque. Los fundamentos del desarrollo de software no cambian por la incorporación de IA generativa.

## Instrucciones personalizadas en este repositorio

Los ejercicios anteriores te mostraron cómo funcionan las instrucciones personalizadas y cómo orientan a Copilot. Si ya realizaste el ejercicio de instrucciones personalizadas, habrás visto `.github/copilot-instructions.md` en acción; si no, este es un buen momento para revisarlo. Antes de asignar trabajo al agente en la nube, realiza una lectura de los archivos de instrucciones incluidos en el repositorio para anticipar su efecto.

Abre los siguientes archivos en la interfaz web de GitHub o en un codespace:

- `.github/copilot-instructions.md`: revisa la sección **Code standards**, especialmente las convenciones de TypeScript y los comentarios TSDoc.
- `.github/instructions/unit-tests.instructions.md`: observa el frontmatter `applyTo`, que limita estas instrucciones a archivos `**/*.test.ts`.

Cuando asignes la incidencia `Code lacks documentation` en la siguiente sección, presta atención a los comentarios TSDoc, las convenciones de TypeScript y los encabezados de comentarios que aparecen en la solicitud de incorporación de cambios. Los revisaremos de nuevo en un ejercicio posterior.

## Configura el entorno de desarrollo del agente en la nube

Crear código siempre necesita un entorno específico y algunos scripts de configuración, independientemente de quién los ejecute. Esto también ocurre al asignar tareas a Copilot.

El agente en la nube utiliza [GitHub Actions][github-actions] como entorno. Puedes personalizarlo mediante un [flujo de trabajo de configuración especial][setup-workflow], definido en `.github/workflows/copilot-setup-steps.yml`, que se ejecuta antes de que el agente empiece a trabajar. Esto proporciona las herramientas y dependencias necesarias. El laboratorio ya incluye esta configuración para que Copilot tenga acceso a Node.js, las dependencias del proyecto, los navegadores de Playwright para las pruebas de extremo a extremo y la base de datos SQLite migrada y poblada de la aplicación Astro:

```yaml
name: "Copilot Setup Steps"

# Permite probar los pasos de configuración desde la pestaña «Actions» del repositorio
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # Establece los permisos mínimos necesarios para tus pasos. Copilot recibirá su propio token para las operaciones.
    permissions:
      # Si quieres clonar el repositorio como parte de los pasos de configuración, por ejemplo para instalar dependencias, necesitarás el permiso `contents: read`. Si no lo haces, Copilot clonará el repositorio automáticamente al finalizar los pasos.
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # Configuración del frontend y la aplicación: Node.js (la aplicación completa utiliza Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # Migra y carga datos en la base de datos SQLite local para que las compilaciones y las pruebas tengan datos.
      - name: Set up the database
        run: npm run db:setup
```

El archivo parece otro flujo de trabajo de GitHub Actions, pero tiene puntos clave:

- Contiene un único trabajo llamado `copilot-setup-steps`.
- El desencadenante `workflow_dispatch` permite ejecutar el flujo de trabajo manualmente desde la pestaña **Actions**.

## Añade documentación

La documentación es importante, pero muchos proyectos tienen información obsoleta o carecen de ella. Ese tipo de deuda técnica reduce la productividad y dificulta la incorporación de nuevas personas. Copilot puede crear documentación y esta incidencia es perfecta para asignarla al agente en la nube.

1. Navega hasta tu repositorio en github.com en una pestaña nueva.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue**.
4. Selecciona **Blank issue**.
5. Establece el título en `Code lacks documentation`.
6. Establece la descripción en:

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. Selecciona **Create**.
8. En la parte derecha, selecciona **Assign to Copilot**.

  ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

9. Selecciona **Assign**.
10. Selecciona la pestaña **Pull Requests**.
11. Abre la solicitud de incorporación de cambios creada, cuyo título podría ser `[WIP]: Code lacks documentation`.
12. Espera unos minutos: es posible que Copilot cree una lista de tareas.

> [!NOTE]
> Puede tardar varios minutos en aparecer la lista de tareas de Copilot.

13. Revisa la lista y las tareas que completará.
14. Observa la línea temporal y, después, selecciona **View session**.

  ![Vista de la sesión de Copilot](../../../_images/ex4-view-session.png)

> [!CAUTION]
> Puede que tengas que actualizar la ventana para ver el indicador actualizado.

16. Revisa la sesión en directo para ver cómo Copilot analiza el proyecto y se plantea un enfoque.

## Añade una sección de juegos relacionados

Asignemos otra tarea al agente en la nube mientras nos ocupamos de otra parte del taller.

1. Vuelve al repositorio en github.com.
2. Selecciona **Issues**.
3. Selecciona **New issue**.
4. Selecciona **Blank issue**.
5. Establece el título en `Show related games on the game details page`.
6. Establece la descripción en:

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. Selecciona **Create** y asigna la incidencia a Copilot.

  ![Asignar Copilot a una incidencia](../../../_images/shared-assign-copilot.png)

La segunda solicitud comenzará a ejecutarse en segundo plano. Podemos dedicar nuestra atención a crear y utilizar agentes personalizados.

## Resumen y próximos pasos

Esta lección presentó [el agente de GitHub Copilot en la nube][copilot-agents] y explicó cómo asignar incidencias para realizar trabajo de forma asincrónica.

Con el agente trabajando en segundo plano, continuaremos con la creación y utilización de agentes personalizados.

## Recursos

- [Acerca del agente de GitHub Copilot en la nube][copilot-agents]
- [Asignar incidencias de GitHub a Copilot][assign-issue]
- [Buenas prácticas del flujo de trabajo de configuración del agente en la nube][cloud-agent-best-practices]

| [Siguiente lección: Agentes personalizados →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
