# Simulador de servicio asíncrono

Pequeña página estática que simula la carga de datos de un usuario. Al pulsar el botón, muestra un estado de carga y, tras una espera de 800 ms, presenta un resultado exitoso o un error simulado.

## Uso

Abre `index.html` en un navegador. No requiere instalar dependencias ni ejecutar un servidor.

La respuesta se simula en el navegador: se muestra el usuario de ejemplo «Ana» con el rol «estudiante» aproximadamente el 70 % de las veces y un error simulado el resto.

## Archivos

- `index.html`: estructura de la página y mensaje accesible para anunciar el resultado.
- `styles.css`: estilos de la interfaz.
- `script.js`: simulación asíncrona y manejo de estados de éxito y error.
- `.github/workflows/deploy-pages.yml`: despliegue automático a GitHub Pages.
- `AUDITORIA.md`: informe de auditoría técnica independiente.

## Publicación

GitHub Actions publica el contenido de la raíz del repositorio en GitHub Pages cada vez que hay un `push` a `main`. También se puede iniciar manualmente desde la pestaña **Actions**, ejecutando **Deploy to GitHub Pages**.

Sitio publicado: [https://cielo201356.github.io/Semana_4/](https://cielo201356.github.io/Semana_4/)
