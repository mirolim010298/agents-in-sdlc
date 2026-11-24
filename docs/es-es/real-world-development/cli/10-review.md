---
title: "Lección 10 - Resumen y próximos pasos"
description: "Recapitula el flujo de trabajo de Copilot CLI, las dos solicitudes de incorporación de cambios, las personalizaciones reutilizables y otros recursos."
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Has utilizado GitHub Copilot CLI en un flujo de trabajo continuo con Tailspin Toys. Has:

- preparado un Codespace, instalado Copilot CLI, explorado el proyecto y encontrado la incidencia de filtrado precargada;
- añadido puntuaciones de estrellas, revisado el resultado en un navegador con el puerto reenviado y combinado manualmente tu primera solicitud de incorporación de cambios (PR);
- iniciado el trabajo desde la incidencia de filtrado, definido el enfoque en el modo Plan, creado la funcionalidad en el modo Autopilot y revisado el resultado en el modo Interactive;
- orientado al agente mediante instrucciones personalizadas y personalizado la habilidad existente `quality-checks` para ejecutar pruebas unitarias, lint y comprobaciones de tipos;
- añadido el servidor Model Context Protocol (MCP) de Playwright y utilizado un navegador real para explorar el filtrado;
- creado y seleccionado un agente personalizado de control de calidad (QA) para evaluar los requisitos, la cobertura, los resultados de la habilidad y las pruebas del navegador;
- revisado el cambio completo de filtrado y autorizado Agent Merge para la PR;
- explorado comandos de barra para contexto, modelos, uso compartido y delegación opcional a la nube.

## Qué has creado

El taller incluye dos hitos de PR, cada uno en su propia rama creada a partir de `main` actualizado:

1. **Puntuaciones de estrellas:** muestra la puntuación existente `starRating` y un estado explícito de no valorado en las tarjetas de los juegos.
2. **Flujo de filtrado y calidad:** implementa el filtrado, actualiza las instrucciones y aplícalas a la funcionalidad, personaliza el informe de `quality-checks`, crea un perfil de control de calidad e incluye las pruebas asociadas.

Desde la planificación del filtrado hasta la apertura de su PR, utilizaste la misma conversación y rama. Reunimos ese trabajo en una única PR para agilizar el taller.

## Distintos tipos de verificación

Has comprobado el código de varias formas: pruebas automatizadas, inspección propia en el navegador y exploración realizada por Copilot mediante MCP. La habilidad `quality-checks` ejecutó pruebas unitarias, lint y comprobaciones de tipos y presentó los resultados con el nuevo formato. El control de calidad reunió esos resultados con una revisión de los requisitos y la cobertura de las pruebas antes de abrir la PR.

Las pruebas añadidas deben cubrir lagunas reales; una ejecución de control de calidad que no requiera nuevas pruebas puede ser correcta. Revisa el código y las evidencias antes de autorizar la combinación y actualiza las evidencias afectadas después de realizar cambios.

## Buenas prácticas

El contexto y las herramientas que proporcionas a Copilot condicionan su trabajo. En este taller has actualizado instrucciones, personalizado una habilidad, creado un perfil de control de calidad y configurado un servidor MCP. Reutiliza estas personalizaciones entre conversaciones y ajústalas a medida que cambien las necesidades de tu equipo. Las instrucciones establecen normas, las habilidades describen tareas repetibles, los agentes personalizados definen funciones especialistas y los servidores MCP conectan herramientas externas. Revisa los cambios reales y los resultados de las herramientas, no solo el resumen del agente.

Adapta el **modo y el modelo** a la tarea. Utiliza **Plan** para reflexionar sobre un enfoque antes de crear, **Interactive** para mantenerte implicado en cambios específicos y **Autopilot** para tareas con un alcance acotado. Elige un modelo rápido para modificaciones rutinarias y uno más capaz para tareas complejas.

El contexto sigue siendo tan importante como la infraestructura. Describir claramente *qué* quieres crear, *por qué* y *cómo* modifica significativamente el resultado.

## Más opciones para explorar

Ya has cubierto el flujo principal. Otras funciones de CLI interesantes:

- `/review`, para pedir al agente de revisión de código que analice los cambios;
- `/rubber-duck`, para conversar sobre un problema y obtener otra perspectiva;
- `/fleet`, para orquestar subtareas independientes en paralelo;
- `/worktree`, para aislar una tarea independiente;
- `/delegate`, para enviar una tarea al agente de GitHub Copilot en la nube.

## Próximos pasos

La mejor forma de mejorar con cualquier herramienta es seguir utilizándola. Úsala con código de producción, con proyectos personales o con esa pequeña aplicación que llevas años pensando en crear y todavía no has empezado. Comparte tus aprendizajes con tu equipo y aprende de ellos. Y, como siempre, explora la documentación.

Si quieres ampliar Tailspin Toys desde el terminal, continúa con la serie opcional [Foundry Backer Concierge][foundry]. Para comparar otros entornos, explora el [taller de VS Code][vscode], el [taller de la aplicación GitHub Copilot][app] o el [taller del agente de GitHub Copilot en la nube][cloud].

## Recursos

- [Acerca de GitHub Copilot CLI][about-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]
- [Personalizar Copilot CLI][customize-cli]
- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
