---
title: "Lección 8 - Crear y combinar la PR de la funcionalidad"
description: "Revisa conjuntamente el filtrado, las instrucciones, la actualización de la habilidad, el perfil de control de calidad y las pruebas; después crea una PR y utiliza Agent Merge."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

La implementación del filtrado, las actualizaciones de las instrucciones, la actualización de la habilidad, el perfil de control de calidad y las pruebas están guardados en una sola rama. Es hora de revisarlos conjuntamente y abrir una solicitud de incorporación de cambios. Has combinado la solicitud de puntuaciones tú mismo; esta vez dejarás que **Agent Merge** gestione el proceso.

> [!NOTE]
> Normalmente separaríamos la funcionalidad, las actualizaciones de instrucciones, la habilidad y el agente de control de calidad en varias solicitudes de incorporación de cambios. Para agilizar el taller, se ha mantenido todo el flujo de filtrado y calidad en una misma conversación y rama, y todo ese trabajo se incluye en esta PR.

En esta lección:

- aprenderás qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación;
- inspeccionarás el cambio completo de la funcionalidad y las pruebas de verificación;
- crearás la PR del filtrado;
- activarás Agent Merge solo después de la revisión y confirmarás que la PR se ha combinado.

## Escenario

A lo largo del flujo de filtrado has utilizado Copilot para planificar, implementar y verificar una funcionalidad. Tailspin Toys quiere automatizar el trabajo restante de la PR y, al mismo tiempo, mantener la autorización de combinación bajo el control de la persona desarrolladora.

## Presentación de Agent Merge

**Agent Merge** automatiza el trabajo restante necesario para incorporar una solicitud de incorporación de cambios. Cuando lo activas, Copilot trabaja sobre lo que bloquea la PR: corrige las comprobaciones fallidas de integración continua (CI), responde a comentarios de revisión y vuelve a aplicar cambios cuando es necesario. Después activa la combinación automática de GitHub cuando la configuración del repositorio lo permite.

Hasta ahora has seleccionado tú **Merge pull request**. Agent Merge puede asumir esa responsabilidad. Revisa el trabajo y decide si está listo antes de activarlo.

## Utiliza Agent Merge para gestionar la PR

Como ya has creado todo el código, vamos a revisarlo conjuntamente, crear la PR y dejar que Agent Merge gestione el resto del proceso.

1. Vuelve a tu Codespace.
2. Abre el diálogo de agentes introduciendo `/agent`.
3. Selecciona **Default** en la lista y pulsa <kbd>Enter</kbd>.
4. Crea una PR nueva con `/pr create`.
5. Activa Agent Merge con `/pr agentmerge`.
6. Copilot supervisará el proceso de integración continua de la PR. Cuando todo haya finalizado correctamente, realizará la combinación.
7. Busca un mensaje de Copilot parecido a «PR #14 was squash-merged successfully».

> [!IMPORTANT]
> Agent Merge no evita aprobaciones obligatorias, protecciones de rama, colas de combinación, ajustes del repositorio ni permisos faltantes. Si queda bloqueado, lee el motivo indicado y completa manualmente la combinación revisada cuando el repositorio lo permita.

## Resumen y próximos pasos

Has automatizado varias partes del proceso de desarrollo: generación de código, pruebas y validación, y ahora el proceso de solicitud de incorporación de cambios. En concreto:

- aprendiste qué es Agent Merge y cómo automatiza el ciclo de vida de una combinación;
- inspeccionaste el cambio completo de la funcionalidad y las pruebas de verificación;
- creaste la PR del filtrado;
- activaste Agent Merge solo después de la revisión y confirmaste que la PR se había combinado.

A continuación, [explorarás otros comandos de barra útiles de Copilot CLI][next-lesson] para contexto, modelos, compartir sesiones y delegación opcional a la nube.

## Recursos

- [Gestionar solicitudes de incorporación de cambios con Copilot CLI][manage-prs]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
