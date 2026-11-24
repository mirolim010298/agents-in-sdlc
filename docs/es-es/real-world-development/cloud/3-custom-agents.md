---
title: "Ejercicio 3 - Agentes personalizados"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## Qué son los agentes personalizados

[Los agentes personalizados][custom-agents-concept] de GitHub Copilot permiten crear asistentes de IA especializados para tareas o ámbitos concretos del flujo de trabajo de desarrollo. Al definir agentes mediante archivos Markdown en la carpeta `.github/agents` del repositorio, puedes proporcionar a Copilot instrucciones específicas, buenas prácticas, patrones de programación y conocimientos del dominio que orienten su trabajo. Los equipos pueden codificar su experiencia en agentes reutilizables: un agente de accesibilidad que aplique las directrices [WCAG][wcag], un agente de seguridad que siga prácticas de programación segura o un agente de pruebas que mantenga patrones coherentes.

Los agentes personalizados se definen mediante archivos Markdown en `.github/agents` del proyecto o de forma global en `~/.copilot/agents`. Cada archivo tiene frontmatter YAML con al menos `name` y `description`, seguido de un aviso en Markdown que define el comportamiento, la experiencia y las instrucciones del agente.

### Agentes personalizados frente a habilidades de agente

Existe cierta superposición lógica entre los agentes personalizados y las [habilidades de agente][agent-skills-concept]. Ambos se definen principalmente con archivos Markdown y explican a una IA cómo realizar operaciones. La forma más clara de diferenciarlos: un **agente personalizado** es el trabajador y las **habilidades** son sus herramientas.

Los agentes personalizados tienen su propia ventana de contexto y pueden orquestar habilidades e incluso otros agentes para realizar su trabajo.

> [!NOTE]
> No existe una única forma correcta de crear un agente personalizado. Como ocurre con otras funciones de IA, prueba y itera hasta encontrar el enfoque adecuado para tus entornos y escenarios.

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## Escenario

Tailspin Toys quiere garantizar que su plataforma de financiación colectiva sea accesible para todas las personas. Los comentarios recientes indican que algunas tienen dificultades con el tema oscuro actual debido al contraste insuficiente entre el texto y el fondo. El equipo de diseño solicita un modo de alto contraste que las personas puedan activar y desactivar.

## Revisa el agente personalizado de accesibilidad

El repositorio ya incluye un agente personalizado de accesibilidad. Revísalo para comprender cómo orientará a Copilot.

1. Abre `.github/agents/accessibility.md`.
2. Observa el frontmatter YAML con los campos `name` y `description`.

> [!CAUTION]
> Los campos `name` y `description` del frontmatter son obligatorios para los agentes personalizados.

3. Revisa las secciones siguientes:
   - Responsabilidades principales al generar código accesible.
   - Buenas prácticas de accesibilidad.
   - Ejemplos de código HTML, CSS y JavaScript.
   - Problemas y errores habituales.

## Crea y asigna una incidencia

El panel de agentes es el lugar central para trabajar con los agentes de tu entorno. Asigna tareas al agente de GitHub Copilot en la nube y supervisa o redirige su trabajo.

1. Navega hasta tu repositorio.
2. Selecciona la pestaña **Issues**.
3. Selecciona **New issue** y **Blank issue**.
4. Establece el título en `Add high contrast mode to website`.
5. Establece la descripción en:

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

6. Selecciona **Create**.
7. Selecciona **Assign to Copilot**.
8. Selecciona **Accessibility agent**.

    ![Captura de pantalla de la asignación al agente en la nube, con el agente personalizado Accessibility resaltado](../../../_images/ex5-select-custom-agent.png)

9. Selecciona **Assign**.

## Resumen y próximos pasos

Has explorado los [agentes personalizados][custom-agents] y cómo pueden convertir la experiencia y las normas del equipo en instrucciones reutilizables.

A continuación, [supervisarás y dirigirás la sesión del agente][next-lesson] desde el panel de agentes.

## Recursos

- [Acerca de los agentes personalizados][custom-agents]
- [Preparar el uso de agentes personalizados en tu organización][org-custom-agents]
- [Preparar el uso de agentes personalizados en tu empresa][enterprise-custom-agents]

---

| [← Lección anterior: Agente de GitHub Copilot en la nube][previous-lesson] | [Siguiente lección: Supervisar y gestionar agentes →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
