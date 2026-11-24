---
title: "Lección 2 - Añadir puntuaciones de estrellas: una victoria rápida"
description: "Utiliza Copilot CLI para realizar un cambio pequeño en las tarjetas de juegos, revisarlo en un navegador con el puerto reenviado y combinarlo como tu primera solicitud de incorporación de cambios."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Ahora que has instalado Copilot CLI y probado una conversación, es el momento de hacer tu primer cambio en el proyecto. Lo mantendremos pequeño: los juegos ya tienen una puntuación de estrellas en sus datos, pero las tarjetas de la página principal todavía no la muestran. Pedirás al agente que la muestre, revisarás el cambio y lo combinarás como tu primera solicitud de incorporación de cambios.

En esta lección:

- iniciarás una conversación centrada con Copilot en una rama de funcionalidad;
- pedirás al agente que haga un cambio pequeño en el proyecto;
- revisarás el cambio con `/diff`;
- ejecutarás la aplicación para confirmar el cambio en un navegador con el puerto reenviado;
- abrirás y combinarás tu primera solicitud de incorporación de cambios.

## Escenario

Cada juego de Tailspin Toys puede tener una puntuación de estrellas, y esta ya aparece en la página de detalles del juego. Sin embargo, las tarjetas de la página principal solo muestran el título, la categoría, la editorial y la descripción. Como ejercicio inicial, harás que el agente muestre la puntuación existente en cada tarjeta: un cambio pequeño y autónomo, perfecto para tu primera sesión.

## Anatomía de una conversación

Una **conversación** es el lugar donde trabajas con Copilot CLI en una tarea. A diferencia de la aplicación Copilot, una conversación normal de CLI utiliza el repositorio y la rama de Git que tengas activados en el terminal en lugar de crear un árbol de trabajo dedicado. Las conversaciones guardadas permiten volver a la misma conversación más tarde, mientras que los archivos y la rama siguen siendo estado ordinario de Git en el disco.

Dentro de una conversación verás tres elementos: tus mensajes y las respuestas del agente, la actividad de sus herramientas mientras explora y edita archivos y los cambios que puedes inspeccionar con `/diff`.

## Inicia una conversación y solicita el cambio

Empecemos una conversación nueva para implementar la funcionalidad.

1. Vuelve a tu Codespace.
2. Si el terminal no está abierto, pulsa <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) o <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux).
3. Si aún no está abierto, inicia Copilot con el siguiente comando:

   ```bash
   copilot --yolo
   ```

4. Inicia una sesión nueva con el comando de barra `/new` y pulsa <kbd>Enter</kbd>.
5. Utiliza el siguiente mensaje para solicitar el cambio:

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot explora el proyecto, localiza los archivos utilizados para mostrar los detalles de los juegos y crea el código necesario. ¡Ya has añadido una nueva funcionalidad con Copilot CLI!

## Revisa el diff

Todos los cambios generados por IA deben revisarse antes de combinarse, incluso los pequeños. Vamos a explorar los cambios aquí mismo en Copilot CLI.

1. Introduce `/diff` e inspecciona cada archivo modificado.
2. Confirma que la tarjeta muestra la puntuación numérica cuando existe y `No rating yet` cuando `starRating` es `null`.
3. Confirma que las pruebas cubren ambos estados.
4. Revisa los resultados de las comprobaciones ejecutadas por Copilot y pide que corrija cualquier fallo.
5. Cuando termines la revisión, pulsa <kbd>Esc</kbd> para salir de la pantalla de diferencias.

> [!NOTE]
> Como Copilot, al igual que todas las herramientas de IA generativa, es probabilístico en lugar de determinista, el código exacto puede variar. Revisa el comportamiento en lugar de esperar una implementación concreta.

## Comprueba los cambios

No debemos limitarnos a leer el código y suponer que funciona. Pide a Copilot que inicie el sitio web para examinar la interfaz de usuario actualizada en el navegador que se abre mediante el puerto reenviado de Codespaces.

1. Pide a Copilot que inicie la aplicación:

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser**.
3. Confirma que las tarjetas muestran las puntuaciones sobre cinco.
4. Vuelve a Copilot y pide que detenga el servidor iniciado:

   ```plaintext
   Stop the development server you started.
   ```

## Abre y combina tu primera solicitud de incorporación de cambios

Ya has creado la funcionalidad. Es hora de crear una solicitud de incorporación de cambios (PR) para combinar el código nuevo con el proyecto.

1. Pide al agente predeterminado que confirme el cambio:

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. Introduce `/pr create`. Copilot CLI envía la confirmación existente al crear la PR y muestra su URL.
3. Abre la PR manteniendo pulsado <kbd>Command</kbd> (Mac) o <kbd>Ctrl</kbd> (Windows/Linux) y seleccionando la URL mostrada por Copilot CLI.
4. Revisa los archivos modificados y las comprobaciones.
5. Cuando esté lista, selecciona **Merge pull request** y confirma la combinación.
6. Vuelve a tu Codespace y sal de Copilot CLI con `/exit`.
7. Actualiza tu rama local `main`:

   ```bash
   git checkout main
   git pull
   ```

## Resumen y próximos pasos

¡Enhorabuena! Has enviado tu primer cambio con GitHub Copilot CLI. En concreto:

- iniciaste una conversación centrada con Copilot en una rama de funcionalidad;
- pediste al agente que hiciera un cambio pequeño en las tarjetas de juegos;
- revisaste el cambio con `/diff`;
- ejecutaste la aplicación para confirmar la puntuación en un navegador con el puerto reenviado;
- abriste y combinaste tu primera solicitud de incorporación de cambios.

A continuación, [empezarás desde la incidencia de filtrado y utilizarás los modos Plan y Autopilot][next-lesson] para crear una funcionalidad mayor.

## Recursos

- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
