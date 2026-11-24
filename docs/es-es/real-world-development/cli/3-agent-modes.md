---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Utiliza Plan para acordar un enfoque, Autopilot para crear el filtrado desde una incidencia y el modo Interactive para revisar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Empezamos añadiendo una funcionalidad pequeña al proyecto. Sin embargo, los cambios mayores requieren un proceso más sólido. Por suerte, GitHub Copilot CLI está diseñado para integrarse con el flujo de trabajo existente de una organización y garantizar que creemos lo correcto de la forma adecuada. Esta es la primera de varias lecciones en las que seguirás un proceso típico de desarrollo con agentes: empezarás con una incidencia para generar una nueva funcionalidad, comprobarás que el código sea válido, validarás que la funcionalidad se comporte como se espera y, finalmente, la combinarás con éxito en el proyecto.

> [!NOTE]
> Utilizarás la misma conversación y rama a medida que avances por el flujo de trabajo de la funcionalidad. Normalmente tendrías ramas o solicitudes de incorporación de cambios distintas para los diferentes tipos de archivo, pero aquí tomaremos un atajo para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una conversación nueva con Copilot desde una incidencia de GitHub;
- definirás los requisitos en el modo Plan;
- implementarás la nueva funcionalidad en el modo Autopilot;
- revisarás el código;
- validarás manualmente la funcionalidad en un navegador con el puerto reenviado.

Mientras continúas con esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad existente `quality-checks`, añadirás validación MCP, crearás un agente de control de calidad y abrirás la solicitud de incorporación de cambios de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys está creciendo y las personas visitantes necesitan limitar los juegos por categoría y editorial. La incidencia del backlog describe la funcionalidad, pero se deben acordar detalles como la combinación de categorías antes de programar. Utilizarás el modo Plan para resolver esas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Contexto

La introducción de agentes de programación con IA en el flujo de desarrollo no cambia los fundamentos. Si acaso, los hace todavía más importantes. La mayoría de los desarrolladores siguen un proceso parecido a este:

1. Empezar desde una incidencia registrada que describe el trabajo.
2. Crear un plan de lo que hay que desarrollar.
3. Crear y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la nueva funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Cuando el código se haya revisado y el proceso de integración continua se haya completado, combinarlo.

> [!NOTE]
> Las particularidades exactas varían según el equipo y la organización, aunque casi siempre son una variación de este proceso.

Al seguir este enfoque estándar, te aseguras de que el código generado por IA cumple los requisitos establecidos y pasa por el mismo proceso de revisión que el código escrito a mano.

## Modos de conversación

El **modo de conversación** controla el grado de autonomía del agente. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar de modo:

- **Interactive**: tú y el agente trabajáis juntos. El agente propone cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan y no puede editar los archivos del proyecto.
- **Autopilot**: el agente trabaja de forma autónoma: escribe código, ejecuta pruebas e itera hasta completar la tarea.

Empieza en el modo Plan, revisa el plan y, después, utiliza Autopilot para implementarlo.

## Empieza desde la incidencia

Antes de empezar con el filtrado, vuelve a tu Codespace y asegúrate de que el repositorio y el terminal están preparados.

1. Vuelve a tu Codespace. Si está detenido, reinícialo antes de continuar.
2. Confirma que la PR de puntuaciones de estrellas está combinada.
3. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
4. Actualiza `main` y crea una rama para el filtrado:

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

5. Inicia Copilot CLI:

   ```bash
   copilot --yolo
   ```

6. Pulsa <kbd>Tab</kbd> dos veces para abrir la pestaña **Issues**.
7. Pulsa <kbd>A</kbd> para mostrar todas las incidencias.
8. Utiliza las teclas de dirección para seleccionar la incidencia titulada **Allow users to filter games by category and publisher**.
9. Pulsa <kbd>C</kbd> para añadir la incidencia al mensaje y volver a la pestaña **Session**.

Observa que el mensaje ahora empieza por `#7` (o un número similar). El símbolo `#` permite incorporar al contexto una incidencia o solicitud de incorporación de cambios (PR) de GitHub.

## Planifica la funcionalidad de filtrado

La planificación te permite definir el enfoque para implementar una funcionalidad o realizar tareas antes de entregarlas a Copilot. Para cualquier trabajo complejo, dedicar un poco de tiempo a planificar siempre es una buena idea. Cambia al modo Plan y pide a Copilot que cree el plan.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para cambiar al modo Plan. Confirma que el indicador situado debajo del mensaje muestra **Plan**.
2. Después de la referencia a la incidencia añadida en el paso anterior, introduce el siguiente mensaje:

   ```plaintext
   Create a plan for implementing this feature.
   ```

Copilot comienza a elaborar el plan: primero explora el proyecto y después determina el mejor enfoque.

3. Puede que Copilot haga preguntas sobre cómo deben funcionar los filtros. Respóndelas según tus preferencias. ¡Aquí no hay respuestas incorrectas!
4. Cuando esté completo, pulsa <kbd>Control</kbd>+<kbd>E</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) para ampliar el plan.
5. Desplázate hacia arriba y hacia abajo para revisarlo.
6. Pide a Copilot que revise cualquier parte que no coincida con tus decisiones.

## Aprueba Autopilot

Con el plan escrito y revisado, ya puedes implementarlo. Dejemos que Copilot haga su trabajo con Autopilot.

Autopilot permitirá a Copilot iterar sobre el problema hasta considerar que está completo.

1. Selecciona **Accept plan and build on autopilot (recommended)**, o la opción con nombre similar de la versión instalada.
2. Confirma que el indicador situado debajo del mensaje muestra **Autopilot**.
3. Observa cómo Copilot sigue el plan establecido, genera código y ejecuta pruebas.

> [!NOTE]
> La aprobación puede iniciar la implementación de inmediato, así que revisa el plan antes. Si Copilot informa de dependencias que faltan o de un conflicto de puerto, resuelve el problema de configuración antes de dar por completadas las comprobaciones.

## Revisa y verifica la implementación

Cuando se genera el código, debe revisarse antes de combinarse, igual que cualquier otro código. Revisa el código y ejecuta el sitio para confirmar que todo funciona.

1. Pulsa <kbd>Shift</kbd>+<kbd>Tab</kbd> para entrar en el modo Interactive. Confirma que el indicador ya no muestra **Plan** ni **Autopilot**.
2. Introduce `/diff` e inspecciona la implementación del filtrado y las pruebas.
3. Compara el resultado con la incidencia y las decisiones tomadas durante la planificación.
4. Cuando hayas terminado la revisión, pulsa <kbd>Esc</kbd> para salir de la vista de diferencias.
5. Revisa la salida de las comprobaciones del proyecto y pide a Copilot que resuelva los fallos.

## Explora la nueva funcionalidad

El código tiene buena pinta, pero ¿se ejecuta? Inicia la aplicación como hiciste antes y abre el sitio mediante el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Prueba el filtrado por categoría, por editorial y las combinaciones acordadas en el plan.
4. Confirma que el restablecimiento y el comportamiento sin resultados coinciden con la incidencia y tus decisiones.
5. Vuelve a tu Codespace y pide a Copilot que detenga el servidor de desarrollo iniciado.

## Resumen y próximos pasos

Has utilizado diferentes modos de conversación para crear y revisar una funcionalidad. En esta lección:

- iniciaste una conversación nueva con Copilot desde una incidencia de GitHub;
- definiste los requisitos en el modo Plan;
- implementaste la nueva funcionalidad con el modo Autopilot;
- revisaste el código;
- validaste manualmente la funcionalidad en un navegador con el puerto reenviado.

A continuación, profundizaremos en cómo se genera el código y cómo sigue las prácticas documentadas mediante [instrucciones personalizadas][next-lesson].

## Recursos

- [Autopilot en GitHub Copilot CLI][autopilot]
- [Referencia de comandos de Copilot CLI][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
