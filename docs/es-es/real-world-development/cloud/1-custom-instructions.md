---
title: "Ejercicio 1 - Instrucciones personalizadas (Agente en la nube)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Agente en la nube →][next-lesson]

El contexto es clave cuando se trabaja con IA generativa. Si una tarea debe realizarse de una forma concreta o si hay información de fondo que Copilot debe conocer, debes asegurarte de que ese contexto esté disponible. Los [archivos de instrucciones][instruction-files] permiten proporcionar esa orientación.

En este ejercicio:

- Explorarás cómo las instrucciones personalizadas del repositorio y los archivos de instrucciones con ámbito por ruta hacen llegar a Copilot el contexto específico del proyecto, las normas de programación y los estándares de documentación.
- Añadirás una nueva norma para todo el repositorio en `.github/copilot-instructions.md`.

> [!NOTE]
> A diferencia de los recorridos de VS Code y CLI, aquí no ejecutarás un aviso de «antes/después»: el agente de GitHub Copilot en la nube trabaja de forma asincrónica sobre incidencias de GitHub, por lo que su efecto es más difícil de demostrar en tiempo real. Verás la influencia del archivo de instrucciones al revisar las solicitudes de incorporación de cambios que produzca el agente en la nube.

## Archivos de instrucciones

### Escenario

Como cualquier empresa de desarrollo responsable, Tailspin Toys tiene una serie de directrices y requisitos para sus prácticas de desarrollo:

- La capa de datos siempre necesita pruebas unitarias.
- La interfaz debe tener un tema oscuro y una estética moderna.
- Debe añadirse documentación al código mediante comentarios TSDoc.
- Debe añadirse un bloque de comentarios al principio de cada archivo que describa su finalidad.

Mediante los archivos de instrucciones, te asegurarás de que Copilot dispone de la información adecuada para realizar las tareas de acuerdo con estas prácticas.

### Instrucciones personalizadas

Las instrucciones personalizadas permiten proporcionar contexto y preferencias a Copilot para que comprenda mejor el estilo de programación y los requisitos. Puedes crear instrucciones para todo el repositorio o para tipos concretos de archivos y tareas.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, un único archivo de instrucciones que se envía a Copilot en **cada** solicitud relacionada con el repositorio. Contiene información de nivel de proyecto: contexto relevante para la mayoría de las solicitudes realizadas en Chat o CLI, la pila tecnológica, una descripción general de lo que se está creando, buenas prácticas y orientación general.
- Los archivos `.github/instructions/*.instructions.md` pueden crearse para tareas o tipos de archivos específicos. Permiten establecer directrices para lenguajes como TypeScript o Astro, o para tareas como crear un componente de interfaz o una nueva serie de pruebas unitarias.

> [!NOTE]
> Cuando trabajes en el IDE, los archivos de instrucciones solo se utilizan para la generación de código en Copilot Chat, no para las sugerencias de autocompletado ni las de siguiente edición.
>
> Copilot Chat, Copilot CLI y el agente de GitHub Copilot en la nube utilizan tanto los archivos de instrucciones del repositorio como los archivos `*.instructions.md` con frontmatter `applyTo` al generar código.
>
> Por último, Copilot [es compatible con instrucciones que siguen otros estándares][custom-instructions-support], incluidos los archivos AGENTS.md y CLAUDE.md.

### Buenas prácticas para gestionar archivos de instrucciones

Crear una explicación completa de los archivos de instrucciones excede el alcance de este taller. Los ejemplos del proyecto muestran un enfoque representativo. En general:

- Mantén las instrucciones de `copilot-instructions.md` centradas en la orientación de nivel de proyecto, como una descripción de lo que se está creando, la estructura del proyecto y las normas globales de programación.
- Utiliza los archivos `*.instructions.md` para proporcionar instrucciones específicas sobre tipos de archivo (pruebas unitarias, componentes de Astro, capa de datos) o tareas concretas.
- Utiliza lenguaje natural. Haz que las indicaciones sean claras y proporciona ejemplos de cómo debe y no debe ser el código.

No existe una única forma correcta de crear archivos de instrucciones, del mismo modo que no existe una única forma de utilizar IA. La experimentación te ayudará a encontrar lo que mejor funciona para tu proyecto.

> [!TIP]
> Todo proyecto que utilice GitHub Copilot debe contar con una colección sólida de archivos de instrucciones. Mientras exploras los que incluye este proyecto, encontrarás archivos para numerosos tipos de tareas, como [actualizaciones de interfaz][ui-instructions] y [Astro][astro-instructions].
>
> Copilot también puede ayudarte a generar archivos de instrucciones. Cada interfaz los expone de forma diferente (por ejemplo, **Configure Chat → Generate Agent Instructions** en VS Code o `/init` en Copilot CLI); la lección correspondiente indica cómo hacerlo.

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## Explora los archivos de instrucciones de este proyecto

Lee los archivos de instrucciones que incluye este repositorio: hay un archivo principal `copilot-instructions.md` y una colección de archivos `*.instructions.md`. Ábrelos en tu editor o en la interfaz web de GitHub.

1. Abre `.github/copilot-instructions.md`.
2. Examina la breve descripción del proyecto y las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**. En **Code standards**, observa la orientación anidada sobre **GitHub Actions Workflows**.
3. Abre la carpeta `.github/instructions` y examina su contenido. Encontrarás instrucciones para archivos de Astro, la capa de datos Drizzle, pruebas y otros elementos.
4. Abre `.github/instructions/unit-tests.instructions.md`. Observa el campo `applyTo` situado al principio: determina qué archivos deben recibir estas instrucciones. Cualquier archivo de prueba de TypeScript, por ejemplo uno que coincida con `**/*.test.ts`, se incluirá.
5. Examina las instrucciones específicas para crear pruebas unitarias.
6. Por último, abre `.github/instructions/drizzle.instructions.md` y desplázate hasta el final. Observa los enlaces a otros archivos de instrucciones, como `unit-tests.instructions.md`, y a archivos existentes del proyecto.

> [!NOTE]
> La sección **Code formatting requirements** de `copilot-instructions.md` documenta las normas de formato del proyecto, pero todavía no exige documentación dentro del código. En los pasos siguientes, añadirás normas para los comentarios TSDoc y los encabezados de archivos.

## Añade una nueva norma para el repositorio

El siguiente paso es la única edición que realizarás aquí: añade una regla para todo el proyecto que exija que la documentación viva en el código como comentarios TSDoc y como encabezado a nivel de archivo. El agente en la nube tendrá en cuenta esta información cuando trabaje en las incidencias que le asignarás más adelante.

Antes de editar, crea una rama (el agente en la nube leerá las instrucciones desde la rama a la que apunte la incidencia, pero debes confirmar los cambios de forma limpia):

1. Desde el terminal del codespace, crea y cambia a una rama nueva:

   ```bash
   git checkout -b custom-instructions-cloud
   ```

Como hemos visto, `.github/copilot-instructions.md` está diseñado para proporcionar información de nivel de proyecto a Copilot. Vamos a añadir las normas de programación del repositorio para mejorar sus sugerencias.

1. Vuelve a abrir `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**, que debería encontrarse cerca de la línea 27. Observa cómo documenta las normas de programación del proyecto, pero todavía no incluye una regla para la documentación dentro del código.
3. Añade las siguientes líneas justo debajo de las normas existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda `copilot-instructions.md`.

> [!TIP]
> Como viste en la lección anterior, los archivos de instrucciones pueden crearse a nivel de repositorio (`.github/copilot-instructions.md`) para orientaciones generales o como archivos `*.instructions.md` para lenguajes, tipos de archivo o tareas concretas. El archivo de nivel de repositorio es el lugar adecuado para normas generales del proyecto, como la regla de comentarios de documentación que acabas de añadir.

## Confirma, envía y combina la actualización de instrucciones

El agente en la nube lee los archivos de instrucciones desde la rama a la que apunte la incidencia. Cuando asignes una incidencia a Copilot en el siguiente ejercicio, Copilot se ramificará desde `main`, así que los cambios deben llegar a `main` para que los tenga en cuenta.

1. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. Envía la rama:

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. Abre una solicitud de incorporación de cambios desde `custom-instructions-cloud` hacia `main` en github.com y combínala. Después, el agente en la nube leerá estas instrucciones cuando trabaje en las incidencias que le asignemos.

> [!TIP]
> Si prefieres trabajar directamente en `main` para este taller, puedes omitir la rama y confirmar los cambios directamente en `main`. El paso de crear una rama se incluye para que el taller refleje cómo se trabaja en un proyecto real.

## Resumen y próximos pasos

Has explorado cómo Copilot obtiene contexto de los archivos de instrucciones y has añadido una nueva norma para todo el repositorio en `.github/copilot-instructions.md`. Verás esa norma reflejada en las solicitudes de incorporación de cambios que genere el agente en la nube en el resto de este recorrido.

A continuación, [asignarás tu primera incidencia al agente de GitHub Copilot en la nube][next-lesson].

## Recursos

- [Archivos de instrucciones para personalizar GitHub Copilot][instruction-files]
- [Buenas prácticas para crear instrucciones personalizadas][instructions-best-practices]
- [5 consejos para escribir mejores instrucciones personalizadas para Copilot][copilot-instructions-five-tips]
- [Awesome Copilot: colección de archivos de instrucciones y otros recursos][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
