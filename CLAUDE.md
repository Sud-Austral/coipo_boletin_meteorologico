# coipo_boletin_meteorologico — guía para agentes

## Resumen
Repositorio mínimo: publica `index.html`, una app React **ya compilada y minificada** (BMI, Boletín Meteorológico de
Incidente, prototipo MVP), en GitHub Pages. VERIFICADO: no hay código fuente, manifiestos, pruebas ni variables de entorno.

## Estructura
- `index.html` — la aplicación publicada (~279 KB). `bmi-prototipo_1.html` es una copia idéntica.
- `.github/workflows/deploy-pages.yml` — único workflow activo; sube la raíz entera (`path: "."`) a Pages en push a `main`
  y en `workflow_dispatch`.
- `deploy-pages.yml` (raíz) y `Claude outputs/deploy-pages.yml` — copias inertes; la de la raíz difiere de la activa.
- `insumos/` — `00-PROBLEMA.md`, `01-SOLUCION.md`, `MANIFIESTO.yaml`.

## Comandos
No hay build, lint ni tests. Para ver el resultado: abrir `index.html` en un navegador.

## Convenciones y reglas
- Documentación en español. Marcar lo dudoso como INFERIDO o «pendiente de confirmar»; no inventar métricas.
- Todo lo que está en la raíz se publica en Pages: no agregar secretos, datos internos ni archivos de trabajo.
- Cambios a `main` por PR.

## Trampas conocidas
- No edites `index.html` a mano: es salida minificada de un compilador cuyo proyecto original no está aquí
  (ubicación pendiente de confirmar por el equipo).
- Hay tres archivos `deploy-pages.yml`; solo el de `.github/workflows/` se ejecuta.
- Los datos de pronóstico vienen en vivo de Open-Meteo, que devuelve 429 en ráfagas.

## Qué no tocar sin confirmar
`index.html`, `bmi-prototipo_1.html` y el workflow activo: cualquier cambio altera lo publicado.
