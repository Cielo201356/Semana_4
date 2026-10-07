# Auditoría técnica

- **Fecha:** 7 de octubre de 2026
- **Alcance:** revisión estática de `index.html`, `styles.css`, `script.js` y `.github/workflows/deploy-pages.yml`, además de comprobaciones de sintaxis y disponibilidad del despliegue.
- **Tipo:** revisión básica de este sitio demostrativo. No sustituye una auditoría de penetración, pruebas de navegador ni un análisis automatizado de dependencias.

## Resumen ejecutivo

No se identificaron vulnerabilidades críticas, altas ni medias en el alcance revisado. Se anotan dos mejoras de bajo riesgo. La aplicación es una página estática sin backend, formularios, datos sensibles ni dependencias de paquetes de aplicación.

## Hallazgos y recomendaciones

| Severidad | Observación | Recomendación |
| --- | --- | --- |
| Baja | El workflow referencia acciones de terceros por etiquetas mayores (`@v4`, `@v5`), que pueden avanzar a nuevas versiones dentro de esa etiqueta. | Para fijar exactamente el código ejecutado, considerar SHA completos verificados y actualizarlos de forma controlada. |
| Baja | La respuesta de usuario y el fallo son aleatorios y simulados; no se realizan solicitudes a un servicio ni se valida una respuesta remota. | Mantener claro que es una demostración. Si se conecta a un backend, validar los datos recibidos y manejar errores de red y respuestas inesperadas. |
| Nota | No hay una suite de pruebas automatizadas para la interfaz o el comportamiento de éxito y error. | Añadir pruebas si el proyecto crece o se integra con servicios reales. |

## Comprobaciones realizadas

- `node --check script.js`: pasó; no detectó errores de sintaxis.
- La página publicada y los recursos `script.js` y `styles.css` respondieron con HTTP 200.
- Las dos ejecuciones del workflow disponibles durante esta revisión finalizaron correctamente.
- Revisión manual del flujo: el botón muestra el estado de carga, la promesa simula éxito/error tras 800 ms y el `catch` presenta el error en la página.
- `git diff --check`: pasó para los cambios de documentación.

## Controles observados

- Los textos dinámicos se insertan con `textContent`, no como HTML.
- El botón es un control HTML nativo y el resultado usa `aria-live="polite"` para anunciar cambios.
- El workflow declara permisos explícitos para leer el repositorio y publicar Pages (`contents: read`, `pages: write`, `id-token: write`); se ejecuta en `ubuntu-latest` y cancela despliegues anteriores del mismo grupo cuando hay uno nuevo.

## Limitaciones

La revisión no incluye una prueba interactiva en navegador, análisis dinámico, escaneo de vulnerabilidades de acciones/dependencias ni evaluación de accesibilidad con tecnologías de asistencia.
