---
title: "Ejercicio 1 - Instrucciones personalizadas (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← Lección anterior: Requisitos previos][previous-lesson] · [Siguiente lección: Modo agente →][next-lesson]

El contexto es clave al trabajar con IA generativa. Si una tarea debe realizarse de una forma concreta o hay información de fondo que Copilot debe conocer, debes hacer que ese contexto esté disponible. Los [archivos de instrucciones][instruction-files] permiten proporcionarlo.

En este ejercicio:

- Explorarás cómo las instrucciones personalizadas del repositorio y los archivos con ámbito por ruta hacen llegar a Copilot el contexto específico del proyecto.
- Generarás la primera parte de datos para el filtrado con las instrucciones actuales.
- Añadirás una nueva norma a `.github/copilot-instructions.md`.
- Ejecutarás de nuevo el mismo aviso y observarás que el código generado adopta la nueva norma.
- Confirmarás los cambios en `main` para que Copilot pueda utilizarlos en el siguiente ejercicio.

> [!CAUTION]
> El código generado puede diferir de las normas establecidas. Copilot no es determinista. El objetivo es observar la tendencia después de actualizar las instrucciones, no obtener una salida idéntica.

## Archivos de instrucciones

Tailspin Toys cuenta con unas directrices de desarrollo que incluyen pruebas unitarias en la capa de datos, una interfaz con tema oscuro y moderno, comentarios TSDoc y encabezados de archivo.

Hay dos tipos de archivos de instrucciones:

- `.github/copilot-instructions.md`, una instrucción global enviada a Copilot en cada solicitud.
- `.github/instructions/*.instructions.md`, para tareas o tipos de archivo concretos.

> [!NOTE]
> Los archivos de instrucciones se utilizan para la generación de código en Copilot Chat, no para el autocompletado ni las sugerencias de siguiente edición.

[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization

## Explora los archivos de instrucciones

1. Abre `.github/copilot-instructions.md` y revisa las secciones **Agent notes**, **Code standards**, **Scripts** y **Repository Structure**.
2. Abre `.github/instructions` y examina las instrucciones para Astro, Drizzle, pruebas y otros ámbitos.
3. Abre `.github/instructions/unit-tests.instructions.md` y observa el campo `applyTo`.
4. Abre `.github/instructions/drizzle.instructions.md` y revisa los enlaces a otras instrucciones y archivos del proyecto.

> [!NOTE]
> La sección **Code formatting requirements** aún no exige documentación dentro del código. Después añadirás normas para los comentarios TSDoc y los encabezados de archivos.

## Crea una rama

1. Abre una terminal nueva.
2. Crea y cambia a una rama:

   ```bash
   git checkout -b custom-instructions
   ```

## Utiliza Copilot Chat antes de actualizar las instrucciones

> [!TIP]
> Abre el panel de Copilot Chat y selecciona **New Chat**.

1. Cierra las pestañas innecesarias para proporcionar un contexto limpio.
2. Abre `src/lib/publishers.ts`.
3. Selecciona **Agent** en el selector de agentes.

   ![Captura de pantalla del selector de modo agente](../../../_images/shared-chat-mode-selector.png)

4. Envía el siguiente aviso:

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Observa que la función propuesta utiliza el patrón de la capa de datos y que todavía no incluye comentarios TSDoc ni encabezado de archivo.

> [!CAUTION]
> Como Copilot es probabilístico, puede añadir comentarios aunque no estén definidos. Si ocurre, la mejora de consistencia después de actualizar las instrucciones seguirá siendo el objetivo del ejercicio.

## Añade una nueva norma para el repositorio

1. Abre `.github/copilot-instructions.md`.
2. Busca la sección **Code formatting requirements**.
3. Añade, justo debajo de las normas existentes:

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. Guarda el archivo.

## Ejecuta de nuevo el aviso

1. Abre Copilot Chat en una conversación nueva.
2. Vuelve a `src/lib/publishers.ts`.
3. Envía exactamente el mismo aviso anterior.
4. Observa que el archivo ahora comienza con un bloque de comentarios similar a:

   ```typescript
   /**
    * Publisher data-access helpers for the Tailspin Toys Crowd Funding platform.
    * Provides functions to retrieve publisher information from the database.
    */
   ```

5. También debe aparecer un comentario TSDoc antes de la función.

## Confirma y envía la actualización

1. Comprueba el estado:

   ```bash
   git status
   ```

2. Prepara y confirma los cambios:

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   git commit -m "Add doc comment standards and publishers helper foundation"
   git push -u origin custom-instructions
   ```

## Crea y combina una solicitud de incorporación de cambios

Pide a Copilot que encuentre la incidencia relacionada con las instrucciones, cree una solicitud de incorporación de cambios y la asocie a la incidencia:

```plaintext
Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
```

Después, pide a Copilot que combine la solicitud y vuelva a `main`:

```plaintext
Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
```

## Resumen y próximos pasos

Has observado cómo las instrucciones personalizadas afectan al código generado y has creado y combinado una solicitud de incorporación de cambios con ayuda de Copilot.

A continuación, pondrás esas instrucciones en práctica en el [modo agente][next-lesson].

## Recursos

- [Archivos de instrucciones][instructions-docs]
- [5 consejos para escribir mejores instrucciones personalizadas][copilot-instructions-five-tips]
- [Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instructions-docs]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
[awesome-copilot]: https://github.com/github/awesome-copilot
