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

- **Fecha:** 7 de octubre de 2026
- **Alcance:** revisión estática de `index.html`, `styles.css`, `script.js` y `.github/workflows/deploy-pages.yml`, además de comprobaciones de sintaxis y disponibilidad del despliegue. Es una auditoría básica de este sitio demostrativo; no sustituye una auditoría de penetración, pruebas de navegador ni un análisis automatizado de dependencias.

### Resumen ejecutivo

No se identificaron vulnerabilidades críticas, altas o medias en el alcance revisado. Se anotan dos mejoras de bajo riesgo. La aplicación es una página estática sin backend, formularios, datos sensibles ni dependencias de paquetes de aplicación.

### Hallazgos y recomendaciones

| Severidad | Observación | Recomendación |
| --- | --- | --- |
| Baja | El workflow referencia acciones de terceros por etiquetas mayores (`@v4`, `@v5`), que pueden avanzar a nuevas versiones dentro de esa etiqueta. | Para fijar exactamente el código ejecutado, considerar SHA completos verificados y actualizarlos de forma controlada. |
| Baja | La respuesta de usuario y el fallo son aleatorios y simulados; no se realizan solicitudes a un servicio ni se valida una respuesta remota. | Mantener claro que es una demostración. Si se conecta a un backend, validar los datos recibidos y manejar errores de red y respuestas inesperadas. |
| Nota | No hay una suite de pruebas automatizadas para la interfaz o el comportamiento de éxito y error. | Añadir pruebas si el proyecto crece o se integra con servicios reales. |

### Comprobaciones realizadas

- `node --check script.js`: pasó; no detectó errores de sintaxis.
- La página publicada y los recursos `script.js` y `styles.css` respondieron con HTTP 200.
- Las dos ejecuciones disponibles del workflow de GitHub Actions finalizaron correctamente.
- Revisión manual del flujo: el botón muestra el estado de carga, la promesa simula éxito/error tras 800 ms y el `catch` presenta el error en la página.
- `git diff --check`: pasó para los cambios de documentación.

### Controles observados en el código

- Los textos dinámicos se insertan con `textContent`, no como HTML.
- El botón es un control HTML nativo y el resultado usa `aria-live="polite"` para anunciar cambios.
- El workflow declara permisos explícitos para leer el repositorio y publicar Pages (`contents: read`, `pages: write`, `id-token: write`); se ejecuta en `ubuntu-latest` y cancela despliegues anteriores del mismo grupo cuando hay uno nuevo.

**Limitaciones:** las comprobaciones no incluyen una prueba interactiva en navegador, análisis dinámico, escaneo de vulnerabilidades de acciones/dependencias ni evaluación de accesibilidad con tecnologías de asistencia.
