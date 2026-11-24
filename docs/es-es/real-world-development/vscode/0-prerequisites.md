---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios de VS Code, prepara el entorno. Crearás tu propia copia del repositorio Tailspin Toys, pondrás en marcha un [codespace][codespaces] y comprobarás que GitHub Copilot Chat funciona en el editor.

## Configura el repositorio del laboratorio

Para crear una copia del repositorio que utilizarás para escribir código, crea una instancia a partir de la [plantilla][template-repository]. La nueva instancia contendrá todos los archivos necesarios para el laboratorio.

1. En una ventana nueva del navegador, abre la [plantilla Tailspin Toys][tailspin-template].
2. Crea tu propia copia seleccionando el botón **Use this template** y, después, **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si participas en un evento dirigido por GitHub o Microsoft, sigue las instrucciones de los responsables. En caso contrario, crea el repositorio en una organización con acceso a GitHub Copilot.

    ![Configuración del repositorio creado a partir de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta creada (**organization-or-user-name/repository-name**), porque la utilizarás más adelante.

> [!NOTE]
> **Tu backlog está listo**
>
> Al crear el repositorio desde la plantilla, se genera automáticamente un backlog de incidencias de GitHub. Trabajarás con ellas a lo largo del taller; no tendrás que crear las incidencias tú.

## Crea un codespace

1. Navega hasta el repositorio recién creado.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y el botón **+** para crear un codespace.

    ![Crear un codespace nuevo](../../../_images/ex0-create-codespace.png)

[GitHub Codespaces][codespaces] permite escribir, ejecutar y depurar código directamente desde el navegador.

> [!CAUTION]
> Volverás al codespace en un ejercicio posterior. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller puede ejecutarse dentro de un codespace o de un [contenedor de desarrollo local][dev-containers]. Ambos incluyen los requisitos previos necesarios. Si prefieres ejecutarlo en local, abre el repositorio clonado en VS Code y selecciona **Reopen in Container**.

## Utiliza GitHub Copilot Chat y el modo agente

Para acceder al modo agente de Copilot Chat necesitas tener instalada la extensión GitHub Copilot Chat.

> [!TIP]
> Si no tienes la extensión instalada, puedes [instalarla desde Visual Studio Marketplace][copilot-chat-extension]. También puedes abrir la vista de extensiones, buscar **GitHub Copilot Chat** y seleccionar **Install**.

1. Vuelve al codespace.
2. Si no ves Copilot Chat a la derecha del editor, selecciona el icono de Copilot Chat.
3. Escribe `Hello world` en Copilot Chat y pulsa Intro.
4. Si todavía no has iniciado sesión, sigue las instrucciones para autenticarte.

    ![Ejemplo de solicitud de autenticación de Copilot Chat](../../../_images/ex1-copilot-authentication.png)

## Resumen

Has creado una copia del repositorio del laboratorio y preparado el codespace que utilizarás para escribir código.

## Próximo paso

Continúa con el [Ejercicio 1 - Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general de GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
