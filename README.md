# coipo_boletin_meteorologico — BMI, Boletín Meteorológico de Incidente

Laboratorio de meteorología. El repositorio publica, en GitHub Pages, un prototipo (MVP) de una página web que reúne en
una sola pantalla información meteorológica para seguir un incidente y compartirla (título de la página: «BMI – Boletín
Meteorológico de Incidente»). Para quién es exactamente y cómo se usa: pendiente de confirmar por el equipo
(ver [`insumos/00-PROBLEMA.md`](insumos/00-PROBLEMA.md)).

## Qué contiene (VERIFICADO con `git ls-files` y `cmp`)

| Ruta | Qué es |
|---|---|
| `index.html` | La aplicación **ya compilada** (un solo archivo de ~279 KB, minificado). Es lo que se publica. |
| `bmi-prototipo_1.html` | Copia byte a byte de `index.html` (comprobado con `cmp`). |
| `.github/workflows/deploy-pages.yml` | El workflow que **sí se ejecuta**: publica la raíz del repositorio en GitHub Pages. |
| `deploy-pages.yml`, `Claude outputs/deploy-pages.yml` | Copias del workflow fuera de `.github/workflows/`; no se ejecutan y la de la raíz difiere de la activa. |
| `insumos/` | Problema, solución y manifiesto del proyecto. |

**No hay código fuente**: ni `package.json`, ni carpeta `src/`, ni pruebas. El repositorio no permite modificar la
aplicación; solo publicarla. Dónde vive el proyecto original es pendiente de confirmar por el equipo.

## Stack (INFERIDO del bundle, no de fuentes)

React (versión de producción incluida en `index.html`), sin servidor propio ni base de datos. El navegador consulta
`api.open-meteo.com/v1/forecast` y la página enlaza o incrusta Windy, Ventusky, NASA FIRMS, Copernicus, OpenStreetMap,
Google Maps, DMC (meteochile.gob.cl) y SENAPRED; comparte por `api.whatsapp.com/send`.

## Cómo verlo

- En línea: se publica en GitHub Pages con cada push a `main` (o a mano desde la pestaña Actions, `workflow_dispatch`).
  La URL final no la comprobé.
- Local: abrir `index.html` en el navegador. No hay comandos de build, instalación ni pruebas porque no existen en el repo.

## Configuración

Ninguna: no hay variables de entorno ni secretos (VERIFICADO en `.github/workflows/deploy-pages.yml` y en la lista de archivos).

## Aviso sobre el despliegue

El workflow empaqueta `path: "."`, es decir **toda la raíz**: las copias sobrantes (`bmi-prototipo_1.html`, los dos
`deploy-pages.yml` extra, `insumos/`) también quedan publicadas. No hay secretos en ellas, pero es superficie publicada sin
querer. Decidir qué se conserva corresponde al equipo.

## Documentación

- [`CLAUDE.md`](CLAUDE.md) — guía para agentes.
- [`insumos/00-PROBLEMA.md`](insumos/00-PROBLEMA.md) — el problema, reconstruido desde el código.
- [`insumos/01-SOLUCION.md`](insumos/01-SOLUCION.md) — la solución, leída desde el código.
