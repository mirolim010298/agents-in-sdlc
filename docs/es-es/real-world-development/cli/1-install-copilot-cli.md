---
title: "Lección 1 - Instalar GitHub Copilot CLI"
description: "Instala y autentica Copilot CLI en tu Codespace, familiarízate con él y encuentra la incidencia de filtrado precargada."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] es un potente asistente de programación con agentes que se ejecuta en el terminal. Permite explorar bases de código, generar código, ejecutar comandos e interactuar con herramientas externas desde la línea de comandos. También ayuda a delegar tareas, solicitar cambios y mantener la concentración. Como puedes imaginar, el primer paso es instalar la herramienta. Por suerte, puedes hacerlo con herramientas que ya conoces.

En esta lección:

- instalarás GitHub Copilot CLI mediante npm;
- te autenticarás con tu cuenta de GitHub;
- confiarás en el repositorio del taller y probarás una conversación rápida;
- encontrarás la incidencia de filtrado mediante el servidor MCP integrado de GitHub.

## Escenario

Tu equipo está empezando a utilizar agentes de IA para trabajar con un backlog en crecimiento. Copilot CLI lleva esa capacidad al terminal, donde muchos desarrolladores ya trabajan. Esta lección te deja instalado, autenticado y preparado para el resto del taller.

## Instala Copilot CLI

Puedes instalar Copilot CLI mediante [npm][install-cli], WinGet y Homebrew. Como GitHub Codespaces incluye Node.js, utilizarás npm.

1. Vuelve al Codespace y abre un terminal.
2. Comprueba que Node.js esté instalado y cumpla la versión mínima:

   ```bash
   node --version
   ```

   Deberías ver la versión 24 o superior.

3. Instala Copilot CLI globalmente:

   ```bash
   npm install -g @github/copilot
   ```

4. Comprueba la instalación:

   ```bash
   copilot --version
   ```

   Deberías ver el número de versión.

## Autentícate con GitHub

En el primer inicio, Copilot CLI solicitará autenticarse con tu cuenta de GitHub.

1. Inicia Copilot CLI:

   ```bash
   copilot
   ```

2. Si se solicita, sigue las instrucciones del código de dispositivo para autenticarte y autorizar Copilot CLI.
3. Copilot CLI muestra el siguiente mensaje:

   ```plaintext
   Copilot can read files in this folder and, with your permission, edit them or run code and shell commands. It will remember your permissions for the rest of this session.

   Do you trust the files in this folder?
   ```

4. Comprueba que la ruta corresponde al repositorio de Tailspin Toys y responde que sí seleccionando **Yes, and remember this folder for future sessions**.

> [!NOTE]
> En un Codespace, es posible que ya estés autenticado mediante tu sesión de GitHub. Si Copilot CLI inicia sin pedir autenticación, puedes continuar.

## Familiarízate con el entorno

Los comandos escritos en el indicador normal del terminal se ejecutan directamente en el Codespace. Cuando Copilot CLI inicia, el lenguaje natural se envía al agente y los comandos de barra controlan la conversación.

1. Introduce `/model`, utiliza las flechas para seleccionar **Auto**, pulsa <kbd>Enter</kbd> y vuelve a pulsar <kbd>Enter</kbd> para confirmar.
2. Introduce `/help` para ver los comandos disponibles en tu versión instalada y pulsa <kbd>Esc</kbd> para cerrar la ayuda.
3. Haz una pregunta sencilla a Copilot para comprobar que todo funciona:

   ```plaintext
   What are the key files in this project?
   ```

4. Lee la respuesta y observa cómo Copilot explora el repositorio antes de contestar.
5. Introduce `/mcp list` y confirma que el servidor MCP integrado de GitHub está disponible.
6. Pide a Copilot que encuentre la incidencia de filtrado:

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. Abre la URL y lee la incidencia. La utilizarás después de completar un primer cambio rápido.

> [!TIP]
> Una sesión normal de Copilot CLI trabaja en la rama que tenga activada el terminal; no crea automáticamente un árbol de trabajo. Crearás una rama de funcionalidad antes de cada cambio.

## Utiliza el atajo del taller

Normalmente, Copilot CLI pide permiso antes de utilizar herramientas fuera de los permisos establecidos. Para este taller, lo reiniciarás con `--yolo`, un atajo aprobado por el usuario que elimina esas solicitudes de aprobación dentro del Codespace para que puedas concentrarte en los ejercicios.

> [!CAUTION]
> `--yolo` habilita permisos automáticos completos (`--allow-all-tools`, `--allow-all-paths` y `--allow-all-urls`). Utilízalo solo en un entorno aislado como un Codespace o una máquina virtual, y nunca lo conviertas en el comportamiento predeterminado del día a día. Consulta [Permitir y denegar el uso de herramientas][allow-all-warning] para obtener más información.

Para este taller, `--enable-all-github-mcp-tools` activa las herramientas MCP de lectura y escritura de GitHub que utilizarán las lecciones posteriores para trabajar con incidencias y solicitudes de incorporación de cambios. El Codespace limita el acceso al equipo local, aunque los recursos de GitHub autenticados siguen siendo reales. Revisa los cambios antes de publicarlos o combinarlos.

1. Sal de Copilot CLI con `/exit`.
2. Reinícialo desde la raíz del repositorio:

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. Haz otra pregunta rápida sobre el proyecto para confirmar que la conversación funciona y, después, sal con `/exit`.

Copilot guarda las conversaciones automáticamente. Más adelante, después de cambiar las instrucciones o añadir un agente, utilizarás `copilot --resume` para volver a la misma conversación y rama.

## Resumen y próximos pasos

¡Enhorabuena! En esta lección:

- instalaste GitHub Copilot CLI mediante npm;
- te autenticaste con tu cuenta de GitHub;
- confiaste en el repositorio del taller y probaste una conversación rápida;
- encontraste la incidencia de filtrado mediante el servidor MCP integrado de GitHub.

A continuación, [empezarás tu primer cambio centrado][next-lesson] y utilizarás Copilot CLI para mostrar una puntuación de estrellas en las tarjetas de juegos.

## Recursos

- [Instalar GitHub Copilot CLI][install-cli]
- [Acerca de GitHub Copilot CLI][about-copilot-cli]
- [Referencia de comandos de Copilot CLI][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
