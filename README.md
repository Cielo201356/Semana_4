# Simulador de servicio asíncrono

Pequeña página estática que simula la carga de datos de un usuario. Al pulsar el botón, muestra un estado de carga y, tras una espera de 800 ms, presenta un resultado exitoso o un error simulado.

## Uso

Abre `index.html` en un navegador. No requiere instalar dependencias ni ejecutar un servidor.

La respuesta es simulada en el navegador: se muestra el usuario de ejemplo «Ana» con el rol «estudiante» aproximadamente el 70 % de las veces y un error simulado el resto.

## Archivos

- `index.html`: estructura de la página y mensaje accesible para anunciar el resultado.
- `styles.css`: estilos de la interfaz.
- `script.js`: simulación asíncrona y manejo de estados de éxito y error.
- `.github/workflows/deploy-pages.yml`: despliegue automático a GitHub Pages.

## Publicación

GitHub Actions publica el contenido de la raíz del repositorio en GitHub Pages cada vez que hay un `push` a `main`. También se puede iniciar manualmente desde la pestaña **Actions**, ejecutando **Deploy to GitHub Pages**.

Sitio publicado: [https://cielo201356.github.io/Semana_4/](https://cielo201356.github.io/Semana_4/)

## Auditoría del proyecto

**Alcance:** revisión del HTML, CSS, JavaScript y flujo de GitHub Actions. Esta es una revisión estática funcional y de seguridad básica; no sustituye una auditoría de penetración ni una suite de pruebas automatizadas.

### Resultado

- **Críticos/altos:** no se identificaron problemas en el alcance revisado.
- **Medios:** no se identificaron problemas en el alcance revisado.
- **Bajos:** se registran las siguientes observaciones y recomendaciones.

| Severidad | Observación | Recomendación |
| --- | --- | --- |
| Baja | Las acciones de GitHub Actions usan etiquetas de versión (`@v4`, `@v5`) en vez de fijar cada dependencia a un SHA completo. | Para reforzar la integridad de la cadena de suministro, fijar las acciones a SHA verificados y actualizar esos SHA de forma controlada. |
| Baja | La aplicación genera un usuario y un resultado aleatorios; no consulta un servicio real ni valida respuestas de una API. | Mantener explícito que es una demostración. Si se conecta a un backend, validar la respuesta y tratar los errores de red y de datos inesperados. |
| Baja | No hay pruebas automatizadas para la interfaz ni para los resultados exitoso y fallido. | Añadir pruebas si el proyecto evoluciona más allá de esta demostración pequeña. |

### Controles revisados

- Los textos dinámicos se insertan con `textContent`, no como HTML.
- El rechazo de la promesa se captura y se muestra en la interfaz; el elemento de resultado utiliza `aria-live="polite"`.
- El flujo de publicación declara permisos explícitos y limitados al despliegue de Pages (`contents: read`, `pages: write`, `id-token: write`).
- La ejecución inicial de GitHub Actions terminó correctamente y el sitio publicado respondió con HTTP 200.
