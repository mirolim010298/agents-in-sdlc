---
title: "Ejercicio 0: Requisitos previos"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

Antes de empezar los ejercicios del agente de GitHub Copilot en la nube, debes dejarlo todo preparado. Crearás tu propia copia del repositorio Tailspin Toys y pondrás en marcha un [codespace][codespaces] para editar archivos de instrucciones y revisar el trabajo que produzca el agente en la nube.

## Configura el repositorio del laboratorio

Para crear una copia del repositorio que utilizarás para escribir código, crearás una instancia a partir de la [plantilla][template-repository]. La nueva instancia contendrá todos los archivos necesarios para el laboratorio y los utilizarás durante los ejercicios.

1. En una ventana nueva del navegador, navega hasta la [plantilla Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando el botón **Use this template** en la página del repositorio del laboratorio. Después, selecciona **Create a new repository**.

    ![Botón Use this template](../../../_images/ex0-use-template.png)

3. Si realizas el taller como parte de un evento dirigido por GitHub o Microsoft, sigue las instrucciones de los responsables. En caso contrario, puedes crear el nuevo repositorio en una organización en la que tengas acceso a GitHub Copilot.

    ![Configuración del repositorio creado a partir de la plantilla](../../../_images/ex0-repository-settings.png)

4. Anota la ruta del repositorio que hayas creado (**organization-or-user-name/repository-name**), porque tendrás que hacer referencia a ella más adelante.

## Crea un codespace

Ahora utilizarás un codespace para completar los ejercicios del laboratorio.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que te permite escribir, ejecutar y depurar código directamente desde el navegador. Incluye un IDE completo con compatibilidad con varios lenguajes de programación, extensiones y herramientas.

1. Navega hasta el repositorio que acabas de crear.
2. Selecciona el botón verde **Code**.

    ![Selecciona el botón Code](../../../_images/ex0-code-button.png)

3. Selecciona la pestaña **Codespaces** y, después, el botón **+** para crear un codespace nuevo.

    ![Crear un codespace nuevo](../../../_images/ex0-create-codespace.png)

La creación del codespace tardará varios minutos, aunque sigue siendo mucho más rápido que instalar manualmente todos los servicios. Puedes aprovechar este tiempo para explorar otras funciones de GitHub Copilot, a las que prestaremos atención a continuación.

> [!CAUTION]
> Volverás al codespace en un ejercicio posterior. Por ahora, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está preparado para ejecutarse dentro de un codespace o de un [contenedor de desarrollo local][dev-containers]. Ambos garantizan que el entorno tenga todos los requisitos previos necesarios para que la experiencia sea fluida. Si prefieres ejecutarlo en local, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te solicite; VS Code creará el mismo contenedor de desarrollo que utiliza el codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Resumen

¡Enhorabuena! Has creado una copia del repositorio del laboratorio y también has iniciado el proceso de creación de tu codespace, que utilizarás mientras trabajas con el agente de GitHub Copilot en la nube.

## Próximo paso

Vamos a añadir instrucciones personalizadas que seguirá el agente en la nube. Continúa con el [Ejercicio 1 - Instrucciones personalizadas][next-lesson].

## Recursos

- [Información general de GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-custom-instructions/
