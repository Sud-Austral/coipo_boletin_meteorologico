# Problema, reconstruido desde el codigo

## Advertencia sobre la cadena de inferencia

Este documento se escribio hacia atras, desde lo construido. Es la parte mas
debil del ejercicio: el codigo dice que hace el sistema, no que quiso hacer
nadie ni por que. Cada afirmacion lleva su cita o su marca, y ninguna es un
hecho del negocio hasta que alguien del negocio la confirme.

Aqui la advertencia pesa mas que de costumbre, y conviene decirlo de entrada:
**el repositorio no contiene codigo fuente**. Contiene el resultado compilado
de una aplicacion [index.html], un unico archivo de 279 KB con todo el
programa dentro, minificado. El analizador puede leer que direcciones consulta
y que enlaza, pero no puede leer su logica. Todo lo que sigue esta construido
sobre esas señales externas.

## Que problema se estaba resolviendo

[INFERIDO] Habia que reunir en un solo sitio informacion meteorologica que
estaba repartida en muchos. El programa enlaza o incrusta al menos ocho
fuentes distintas desde [index.html]: la Direccion Meteorologica de Chile,
SENAPRED, dos visores de viento —Windy y Ventusky—, el mapa de focos de calor
de NASA FIRMS, el navegador de Copernicus, OpenStreetMap y Google Maps. Reunir
ocho ventanas en una pantalla solo se hace cuando alguien las estaba abriendo
de a una. Cuanto tardaba esa persona, y quien era, es [PENDIENTE].

[INFERIDO] Se necesitaba el pronostico como dato, no como imagen. El programa
consulta una API de pronostico meteorologico
(`api.open-meteo.com/v1/forecast`, citada en [index.html]) en vez de limitarse
a incrustar mapas ajenos. Pedir datos crudos supone que hay que calcular o
presentar algo propio con ellos, no solo mirarlos.

[INFERIDO] El destinatario del producto es un incidente concreto, no el clima
en general. El propio archivo se describe como Boletin Meteorologico de
Incidente [index.html]. "De incidente" acota mucho: el producto se genera
cuando pasa algo, para ese algo. Que se considera un incidente aqui, y quien
lo declara, es [PENDIENTE].

[INFERIDO] El boletin habia que **mandarselo a alguien**, y por telefono. El
programa incluye una salida hacia WhatsApp [index.html]. Eso no se agrega si el
producto se consume solo en un escritorio: se agrega cuando hay que hacerlo
llegar a gente en terreno. A quien, y con que frecuencia, es [PENDIENTE].

[INFERIDO] La combinacion de focos de calor por satelite con pronostico de
viento apunta a incendios forestales, que es ademas el negocio de la
institucion. Pero el codigo no lo dice con esas palabras: lo dice el conjunto
de las fuentes que consulta. Es la inferencia mas razonable de este documento
y sigue siendo una inferencia.

## Quien sufre el problema

[PENDIENTE] No hay roles en este repositorio. No existe autenticacion, ni
permisos, ni usuarios, ni base de datos: es una pagina estatica que se publica
entera [.github/workflows/deploy-pages.yml] y cualquiera con el enlace ve lo
mismo.

[INFERIDO] El area destinataria esta declarada en el propio archivo: la Unidad
de Informacion y Analisis de CONAF [index.html]. Es una declaracion escrita en
una etiqueta de la pagina, no una estructura del sistema.

[PENDIENTE] Cuantas personas lo usan, en cuantos incidentes y con que
frecuencia. No hay analitica ni registro de uso, y al ser una pagina estatica
no hay servidor que pudiera medirlo.

## Como se resolvia antes

[INFERIDO] Abriendo a mano las mismas ocho fuentes que ahora estan reunidas
[index.html]. Es la lectura mas directa de lo que el programa hace, y explica
por que se construyo. Pero el codigo no documenta el procedimiento anterior:
quien lo hacia, con que plantilla y cuanto tardaba es [PENDIENTE].

[PENDIENTE] Si existia un boletin previo en Word, PDF o correo, y que relacion
tiene este con aquel. No hay ningun rastro de migracion ni de formato heredado.

## Que pasa si no se hace nada

[PENDIENTE] Sin excepcion. El codigo no lo responde y no se deduce de que el
sistema exista.

## Volumen

[PENDIENTE] El repositorio no permite estimar ningun volumen. No hay base de
datos, ni indices, ni paginacion, ni tipos de columna: no hay nada de lo que se
suele inferir un orden de magnitud. Cuantos boletines se emiten al ano es una
pregunta que solo responde una persona.

[INFERIDO] Lo que si se puede medir es el tamano del repositorio, y ahi hay un
hallazgo. De sus siete archivos, **cuatro son duplicados exactos de otros dos**,
comprobado por identificador de contenido, no por parecido:

  - [bmi-prototipo_1.html] es byte a byte el mismo archivo que [index.html]:
    273 KB repetidos.
  - [deploy-pages.yml], en la raiz, es byte a byte el mismo archivo que la
    copia que hay bajo una carpeta llamada "Claude outputs". Ninguna de las dos
    es la que se ejecuta: la activa es
    [.github/workflows/deploy-pages.yml], que ademas es distinta de ambas.

Esto no es una conclusion sobre que sobre: es una deteccion. Importa por una
razon concreta, que va en el documento siguiente.

## Quien decide que esta terminado

[PENDIENTE] Sin excepcion. No hay criterio de aceptacion escrito en ninguna
parte del repositorio.

[INFERIDO] El propio archivo se declara prototipo MVP [index.html], asi que
alguien ya decidio que **no** esta terminado. Que falta para que lo este es
[PENDIENTE].

[VERIFICAR] El [README.md] tiene 59 bytes y no describe el proyecto. El sitio
esta publicado y accesible, pero quien llegue al repositorio no encuentra que
es, quien lo mantiene ni bajo que condiciones se puede usar. No hay archivo de
licencia. En un repositorio publico de un organismo del Estado, eso es una
pregunta para Fiscalia.

## Pendientes, y a quien preguntarle cada uno

| Pregunta | A quien |
|---|---|
| Quien pidio el boletin y para que decision se usa | Unidad de Informacion y Analisis |
| Que se considera un incidente y quien lo declara | Unidad de Informacion y Analisis |
| A quien se le manda por WhatsApp y con que frecuencia | quien opera el boletin |
| Como se hacia antes y cuanto tardaba | quien lo hacia |
| Cuantos boletines se emiten al ano | Unidad de Informacion y Analisis |
| Que falta para que deje de ser prototipo | autor del repositorio |
| **Donde esta el codigo fuente de la aplicacion** | autor del repositorio |
| Cual de los tres archivos de despliegue es el bueno | autor del repositorio |

## Verificar, y quien los cierra

| Afirmacion | Quien la cierra |
|---|---|
| Condiciones de uso de las fuentes externas que consulta, y si se puede redistribuir su informacion | Fiscalia |
| Licencia de un repositorio publico sin archivo de licencia | Fiscalia |
| Si el boletin puede usarse como insumo de una decision operativa siendo un prototipo declarado | Unidad de Informacion y Analisis |
