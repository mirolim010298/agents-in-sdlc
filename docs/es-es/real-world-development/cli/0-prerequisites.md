---
title: "Lección 0 - Requisitos previos"
description: "Crea tu propia copia de Tailspin Toys y prepara un Codespace de GitHub para el taller de Copilot CLI."
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Antes de empezar las lecciones de Copilot CLI, debes dejarlo todo preparado. Crearás tu propia copia del repositorio Tailspin Toys y pondrás en marcha un [Codespace][codespaces], cuyo terminal integrado utilizarás para instalar y ejecutar Copilot CLI en la siguiente lección.

En esta lección:

- crearás tu propia copia del proyecto Tailspin Toys a partir de la plantilla;
- crearás un Codespace y confirmarás que el proyecto está listo.

## Configura el repositorio del laboratorio

Trabajarás con tu propia copia del proyecto Tailspin Toys. Créala ahora a partir del [repositorio de plantilla][tailspin-template]. El nuevo repositorio contiene todos los archivos que necesita el laboratorio.

1. En una ventana nueva del navegador, navega hasta la [plantilla de Tailspin Toys][tailspin-template].
2. Crea tu propia copia del repositorio seleccionando **Use this template** y después **Create a new repository**.
3. Si realizas el taller como parte de un evento dirigido por GitHub o Microsoft, sigue las instrucciones de los responsables. En caso contrario, crea el nuevo repositorio en una organización donde tengas acceso a GitHub Copilot.
4. Anota la ruta del repositorio que hayas creado (`organization-or-user-name/repository-name`), porque la utilizarás más adelante.

> [!NOTE]
> Cuando creas el repositorio a partir de la plantilla, se genera automáticamente un backlog de incidencias de GitHub. Trabajarás con esas incidencias a lo largo del taller; no tendrás que crear ninguna tú.

Utiliza una copia nueva de la plantilla del taller. Incluye instrucciones del repositorio, código de la aplicación, pruebas, una habilidad `quality-checks` y el backlog que utilizarás. Si utilizas una copia antigua, consulta con el responsable si contiene los archivos necesarios.

## Crea un Codespace

Ahora utilizarás un Codespace para completar el taller.

[GitHub Codespaces][codespaces] es un entorno de desarrollo basado en la nube que permite escribir, ejecutar y depurar código directamente desde el navegador. Proporciona un editor completo con compatibilidad para varios lenguajes de programación, extensiones y herramientas.

1. Navega hasta el repositorio recién creado.
2. Selecciona **Code**.
3. Selecciona la pestaña **Codespaces** y después **Create codespace on main**.
4. Espera a que finalice la configuración del Codespace. La plantilla instala las dependencias del proyecto, Chromium para Playwright y la base de datos local.
5. Si aparece la pregunta **Do you trust the authors of the files in this folder?**, selecciona **Trust Folder & Continue**.
6. Abre un terminal en la raíz del repositorio y inicia la aplicación:

   ```bash
   npm run dev
   ```

7. Cuando Codespaces indique que el puerto `4321` está disponible, selecciona **Open in Browser** y confirma que el sitio Tailspin Toys se carga.
8. Vuelve al terminal y detén el servidor de desarrollo con <kbd>Ctrl</kbd>+<kbd>C</kbd>.

## Resumen y próximos pasos

¡Ya tienes el entorno preparado! En esta lección:

- creaste tu propia copia del proyecto Tailspin Toys a partir de la plantilla;
- creaste un Codespace y confirmaste que el proyecto estaba listo.

A continuación, [instalarás GitHub Copilot CLI][next-lesson] en el Codespace y lo autenticarás con tu cuenta de GitHub.

3. Selecciona la pestaña **Codespaces** y, a continuación, selecciona el botón **+** para crear un Codespace nuevo.

    ![Crear un codespace nuevo](../../../_images/ex0-create-codespace.png)

La creación del codespace tardará varios minutos, aunque sigue siendo mucho más rápida que instalar manualmente todos los servicios. Dicho esto, puedes aprovechar este tiempo para explorar otras funciones de GitHub Copilot, a las que prestaremos atención a continuación.

> [!CAUTION]
> Volverás al codespace en un ejercicio posterior. De momento, déjalo abierto en una pestaña del navegador.

> [!NOTE]
> Este taller está diseñado para ejecutarse dentro de un codespace o de un [contenedor de desarrollo][dev-containers] local. Ambos garantizan que el entorno tenga instalados todos los requisitos previos necesarios para disfrutar de una experiencia fluida. Si prefieres ejecutarlo en local, abre el repositorio clonado en VS Code y selecciona **Reopen in Container** cuando se te solicite; VS Code compilará el mismo contenedor de desarrollo que usa el codespace.

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## Resumen

¡Enhorabuena! Has creado una copia del repositorio del laboratorio. También has iniciado el proceso de creación de tu codespace, que usarás cuando empieces a trabajar con Copilot CLI.

## Siguiente paso

Vamos a instalar Copilot CLI y a autenticarlo con tu cuenta de GitHub. Continúa con el [Ejercicio 1 - Instalar GitHub Copilot CLI][next-lesson].

## Recursos

- [Información general de GitHub Codespaces][codespaces]
- [Crear un repositorio a partir de una plantilla][template-repository]
- [Primeros pasos con Codespaces][codespaces-quickstart]

[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
