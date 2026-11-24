---
title: "Ejercicio 5 - Supervisión y gestión de agentes"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← Lección anterior: Agentes personalizados][previous-lesson] |
|:--|

En el modo agente, Copilot explora el código, propone cambios, edita archivos y ejecuta comandos. Copilot Chat te permite supervisar cada operación.

## Monitoriza el progreso

1. Vuelve a la vista de Copilot Chat.
2. Observa las lecturas de archivos, las modificaciones y los comandos.
3. Para cada cambio, selecciona **Keep** para aceptarlo o **Undo** para revertirlo.
4. Utiliza el indicador **Files changed** para ver todos los archivos afectados.

> [!NOTE]
> Si una operación necesita permiso, Copilot mostrará una petición **Allow**. Revisa cada comando antes de aprobarlo.

## Añade el modo claro

Envía al agente el siguiente aviso de seguimiento:

```plaintext
Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
```

Revisa cada modificación mediante **Keep** o **Undo**.

## Revisa el conjunto de cambios

1. Abre la vista **Source Control**.
2. Revisa los archivos modificados.
3. Confirma los atributos ARIA, la navegación mediante teclado, el HTML semántico y el uso de almacenamiento local.
4. Cuando estés satisfecho, prepara y confirma los cambios.

## Resumen y próximos pasos

Has supervisado y dirigido una sesión en curso, aceptando o rechazando cambios y ampliando el alcance con avisos de seguimiento.

En la [próxima lección][next-lesson] publicarás el trabajo como una solicitud de incorporación de cambios y revisarás los cambios.

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
