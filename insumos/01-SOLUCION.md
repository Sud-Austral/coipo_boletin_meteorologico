# Solucion, leida desde el codigo

Este documento suele ser la parte solida del ejercicio, porque el codigo ES la
solucion. Aqui no lo es del todo, y hay que decirlo antes de empezar: el
repositorio guarda la aplicacion **ya compilada** [index.html], no su codigo
fuente. Lo que sigue se dedujo de las direcciones que el archivo contiene y de
lo que declara sobre si mismo. La logica interna no se pudo leer.

## Que hace el sistema

Reune en una sola pantalla la informacion meteorologica que hace falta para
seguir un incidente, y la deja lista para compartir. Se describe a si mismo
como Boletin Meteorologico de Incidente, de la Unidad de Informacion y Analisis
de CONAF, y se declara prototipo MVP [index.html].

Es una pagina que se abre en el navegador. No hay servidor propio, no hay base
de datos y no hay cuentas de usuario: todo el programa viaja dentro del archivo
que se descarga.

## De donde saca la informacion

Esta es la parte que si se puede afirmar con evidencia, porque las direcciones
estan escritas dentro del archivo publicado [index.html]:

**Datos que consulta como programa**

- `api.open-meteo.com/v1/forecast` — un servicio de pronostico meteorologico.
  Es la unica llamada de datos del sistema: el resto son enlaces o
  incrustaciones. [INFERIDO] de ahi salen las cifras del boletin.

**Fuentes que incrusta o enlaza**

| Fuente | Que aporta |
|---|---|
| meteochile.gob.cl | la Direccion Meteorologica de Chile, fuente oficial |
| senapred.cl | emergencias y alertas |
| windy.com y embed.windy.com | visor de viento, incrustado en la pagina |
| ventusky.com | segundo visor meteorologico |
| firms.modaps.eosdis.nasa.gov | focos de calor detectados por satelite |
| browser.dataspace.copernicus.eu | imagenes satelitales europeas |
| openstreetmap.org | cartografia base, incrustada |
| maps.google.com | ubicacion y busqueda |

[INFERIDO] La combinacion de focos de calor por satelite con pronostico de
viento es la que da sentido al conjunto: son los dos datos que gobiernan como
se comporta un incendio. El codigo no escribe la palabra incendio, pero eligio
esas fuentes.

**Salida**

- `api.whatsapp.com/send` [index.html]. [INFERIDO] el boletin se comparte por
  telefono, no solo se mira en pantalla.

## Como se publica

Un workflow toma **la raiz completa del repositorio** y la publica en GitHub
Pages, en cada push a la rama principal o a mano desde la pestana Actions
[.github/workflows/deploy-pages.yml].

Esa decision —publicar la raiz entera— tiene una consecuencia directa que se
trata mas abajo.

## Roles: quien ve que

**No hay roles.** Es un hecho verificable, no una omision de este documento: en
las siete rutas del repositorio no existe ninguna tabla de base de datos,
ningun endpoint propio, ninguna variable de entorno y ningun mecanismo de
autenticacion. La pagina es publica y todo el que llega ve lo mismo.

[INFERIDO] La unica distincion real es entre quien consulta el boletin y quien
lo comparte, y esa segunda no es un permiso: es un boton.

## Que NO hace

Estas ausencias son afirmables porque el analizador reviso la categoria
completa sobre las siete rutas:

- **No guarda nada.** No hay base de datos ni almacenamiento: cada visita parte
  de cero y consulta las fuentes en vivo. Un boletin emitido no queda
  registrado en ninguna parte de este repositorio.
- **No tiene servidor propio.** No hay ningun endpoint. Todo ocurre en el
  navegador de quien mira.
- **No tiene variables de entorno**, asi que no hay configuracion por ambiente:
  lo que se publica es exactamente lo que corre.
- **No tiene pruebas automatizadas.** Ninguna ruta bajo tests/ ni con patron de
  archivo de prueba.
- **No tiene archivo de licencia**, siendo un repositorio publico.
- **No tiene codigo fuente.** Ninguna de las siete rutas es un archivo de
  codigo editable, ni un manifiesto de dependencias, ni un archivo de
  configuracion de compilacion. Esta es la ausencia mas importante y se trata
  aparte.

## El problema del codigo fuente

[INFERIDO] La aplicacion se construyo con React: el archivo publicado contiene
la version de produccion de esa biblioteca [index.html]. Un archivo asi es
**salida de un compilador**, no algo que alguien escriba a mano.

La consecuencia practica: **este repositorio no permite modificar la
aplicacion**. Para cambiar una linea del boletin hace falta el proyecto
original, que no esta aqui. Quien tenga solo este repositorio puede publicar el
prototipo, pero no puede evolucionarlo.

Donde vive ese proyecto original es [PENDIENTE] y es la pregunta mas urgente de
los dos documentos. Mientras no se responda, el sistema depende de una maquina
o una carpeta que el repositorio no nombra.

## Archivos repetidos, y por que importa aqui mas que en otros repositorios

De las siete rutas, cuatro forman dos pares de duplicados **exactos**,
comprobados por identificador de contenido:

- [bmi-prototipo_1.html] es el mismo archivo que [index.html], byte a byte.
  273 KB repetidos.
- [deploy-pages.yml], en la raiz, es el mismo archivo que la copia guardada
  bajo una carpeta llamada "Claude outputs" —cuyo nombre lleva un espacio y por
  eso no se puede citar con el formato de este documento—. Y **ninguna de las
  dos es la que se ejecuta**: la activa es
  [.github/workflows/deploy-pages.yml], que ademas difiere de ambas.

Por que importa mas que en otro repositorio: el despliegue publica la raiz
entera [.github/workflows/deploy-pages.yml]. Es decir, **los archivos sobrantes
tambien se publican**. Cualquiera puede descargar del sitio las dos copias del
archivo de despliegue y la copia del prototipo.

No es una fuga de datos —no hay secretos ahi dentro— pero si es superficie
publicada sin querer, y una ambiguedad real: con tres archivos de despliegue
distintos, quien venga despues no sabra cual editar.

Esto es una **deteccion, no una conclusion**. Que sobra y que se conserva lo
decide una persona. Cuando el generador automatico produzca `delete_files.md`
en este repositorio, ahi estara la propuesta con el detalle.

## Iteraciones

[INFERIDO] El nombre [bmi-prototipo_1.html] sugiere una serie —un prototipo 1
implica que se esperaba un 2— pero hoy su contenido es identico al del
[index.html] publicado, asi que no representa una version distinta. Es una
copia, no una iteracion conservada.

[INFERIDO] El sistema se declara MVP [index.html], o sea que quien lo escribio
lo considera una primera version deliberada, no un producto terminado.

## Lo que este borrador no pudo describir

- **Que muestra exactamente el boletin.** Es lo mas importante y es justo lo
  que falta: la logica esta minificada dentro de [index.html] y el analizador no
  la lee. Que variables presenta, con que umbrales, para que ventana de tiempo
  y con que formato, no se puede afirmar desde aqui.
- **Como se elige el lugar del incidente.** Hay cartografia y busqueda, pero no
  se puede saber si la ubicacion se escribe, se pincha en el mapa o llega por
  parametro.
- **Que hace con la respuesta del servicio de pronostico.** Se sabe que lo
  consulta; no se sabe que calcula.
- **El texto del mensaje que se comparte.** Existe la salida hacia WhatsApp; su
  contenido esta dentro del bundle.
- **Si el prototipo se probo con alguien.** No hay ninguna evidencia de uso,
  validacion ni retroalimentacion en el repositorio.
