---
title: "Lección 12 - Publica el sitio con GitHub Pages"
description: "Utiliza la aplicación GitHub Copilot para configurar un flujo de trabajo de Pages, revisar su solicitud de incorporación de cambios y comprobar el Space Quiz publicado."
authors:
  - jamesmontemagno
lastUpdated: 2026-10-12
---

Da al Space Quiz una ubicación pública mediante su publicación con GitHub Pages. Copilot puede preparar el flujo de trabajo y guiar el despliegue, pero tú eres responsable de revisar los cambios y confirmar que el sitio esté activo.

En esta lección:

- Pedirás a Copilot que configure un despliegue con GitHub Pages.
- Revisarás el flujo de trabajo y la solicitud de incorporación de cambios antes de combinarla.
- Seguirás el despliegue y comprobarás el sitio publicado.

## Escenario

El Space Quiz ya está en un repositorio de GitHub, pero las personas necesitan una forma sencilla de probarlo. Publicar el sitio de archivo único con GitHub Pages lo hace disponible desde una URL pública sin añadir un servidor ni una dependencia de entorno de ejecución.

## Pide a Copilot que prepare el despliegue

> [!WARNING]
> Crear una solicitud de incorporación de cambios puede confirmar y enviar código. Revisa la configuración de aprobaciones y el repositorio de destino antes de enviar esta instrucción. Con **Aprobar todo**, no esperes una confirmación independiente.

En la sesión de la aplicación Copilot para `space-quiz`, envía esta instrucción:

```plaintext
Prepare a GitHub Pages deployment for this repository. Create a GitHub Actions workflow that builds the website if needed and deploys it to GitHub Pages after changes reach the default branch. Add a README describing the app and how to run it locally if one does not already exist. Create a pull request with these changes and report its link and any required Pages settings or permissions. Do not merge, enable auto-merge, change Pages settings, or deploy. Stop and wait for my review.
```

## Revisa el flujo de trabajo y la solicitud de incorporación de cambios

1. Confirma que el README solo se añade si el repositorio todavía no tiene uno.
2. Revisa los cambios de la solicitud de incorporación de cambios, incluidos los pasos de compilación y despliegue del flujo de trabajo, los desencadenantes y los permisos.
3. Confirma que el flujo de trabajo se despliega desde la rama predeterminada, no desde una solicitud de incorporación de cambios sin combinar.
4. Solicita las correcciones necesarias y revisa el diff actualizado. Espera a que superen las comprobaciones obligatorias antes de autorizar la combinación.

## Autoriza la combinación y el despliegue

> [!WARNING]
> La siguiente instrucción autoriza al agente a combinar la solicitud de incorporación de cambios revisada, cambiar la configuración de Pages del repositorio y publicar el sitio. Envíala solo después de completar la revisión y confirmar el repositorio y la solicitud de incorporación de cambios. La configuración de aprobaciones puede permitir estas acciones sin otro aviso de confirmación.

Sustituye `<PR_NUMBER>` por el número de la solicitud de incorporación de cambios revisada y envía esta instrucción independiente:

```plaintext
I have reviewed pull request <PR_NUMBER> in this repository and authorize its merge and deployment. Enable GitHub Pages using GitHub Actions, merge that pull request only after required checks pass, and monitor the deployment until it succeeds. Report the final URL of the live website. If you lack permission to enable Pages or merge, tell me exactly what I need to approve or do; do not report success until the site is live.
```

![Diagrama de tres etapas: una solicitud de incorporación de cambios de space-quiz combinada; una ejecución de GitHub Actions Deploy website correcta, con los pasos Build website, Upload artifact y Deploy to Pages; y el Space Quiz publicado en yourname.github.io/space-quiz/.](../../../_images/first-steps-app-pages-deploy.svg)

## Comprueba el despliegue

1. Sigue la ejecución de despliegue de GitHub Actions hasta que finalice correctamente.
2. Abre la URL indicada y confirma que el Space Quiz se carga.

Si el agente no puede activar Pages ni combinar la solicitud de incorporación de cambios, sigue las instrucciones específicas que te proporcione. No des por completa la tarea hasta que el despliegue tenga éxito y el sitio publicado se cargue.

## Resumen y próximos pasos

Tu Space Quiz ya está disponible como sitio activo y has comprobado el despliegue en lugar de confiar únicamente en el informe del agente. Continúa con la [Lección 13: Repaso y próximos pasos][next-lesson].

[next-lesson]: ../13-review/
