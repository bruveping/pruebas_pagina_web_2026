
# Introducción

`alphaTex` es un formato de notación en texto plano para alphaTab. Se escribe una partitura como código fuente y alphaTab la analiza para convertirla en el mismo modelo de datos que generan otros formatos.

Para habilitar la carga de alphaTex, configura la opción `tex`, o bien pasa una cadena de texto directamente a través del método `tex()` de la API. alphaTab lee el código fuente desde el contenido del elemento y lo procesa. También es posible cargarlo desde un archivo, del mismo modo que se hace con cualquier otro formato.

alphaTex abarca la mayoría de las funciones de notación compatibles con alphaTab. Si falta alguna función que necesites, abre un hilo de discusión en GitHub.

Comienza por la **sintaxis del lenguaje**; en ella se definen todos los términos que se utilizan en el resto de esta sección.

## Ejemplo

El siguiente ejemplo se genera completamente a partir de código fuente en alphaTex: se trata de la parte de guitarra solista de la sección *"Intro Build"* de **Iron Waltz**, la canción de demostración de alphaTab.

```js
\title "Iron Waltz"
\subtitle "Intro Build"
\artist "alphaTab"
\tempo 196
\track ("Lead Guitar" "Lead Gtr.") { instrument distortionguitar }
\tuning (Eb4 Bb3 Gb3 Db3 Ab2 Eb2)
\ts (3 4)
\section "Intro Build"
7.1.4{dy f} 14.1.8 12.2 14.2 12.2 |
:16 11.1{b (0 2)} -.1{b (2 0)} :8 11.1 12.2.4 :8 11.1 12.1 |
:16 11.1{h} 12.1{h} :8 11.1 12.2 14.2 16.2 14.2 |
2.1.4 4.1 6.1{v} |
7.1.4 7.2.8 7.1 9.1 7.1 |
:16 11.1{b (0 2)} -.1{b (2 0)} :8 11.1 12.2.4 :8 11.1 12.1 |
11.1.8 12.1 11.1 9.1 7.1 6.1 |
2.1.4 4.1 6.1{v}
```
# Sintaxis del lenguaje
Esta página describe la sintaxis del código fuente de alphaTex y define el vocabulario que se utiliza en el resto de la referencia. Todas las demás páginas enlazan con los enlaces de esta página la primera vez que se utiliza un término. Guarde el código fuente de alphaTex con la extensión de archivo .atex.

## Comentarios
Úselos //para comentarios de línea y /* ... */para comentarios de bloque. Colóquelos en cualquier parte de un archivo alphaTex para anotar su código fuente.
```js
// This is a single-line comment.
/* This is a
   multi-line block comment. */
```
  ## Cadenas de caracteres
   Encierre los valores de texto entre comillas dobles o simples.
```js
   "Double quoted string"
   'Single quoted string'
```
   Las siguientes secuencias de escape son compatibles dentro de los literales de cadena:

   \n— salto de línea
   \r— retorno de carro
   \t— pestaña
   \\— una barra invertida literal
   \'y \"— una cita literal
   \uXXXX— un punto de código Unicode expresado como cuatro dígitos hexadecimales
  ## Números
   alphaTex admite números enteros y decimales. Los números decimales solo se aceptan en los lugares donde no puedan entrar en conflicto con la notación de notas de traste o los valores de duración.

  ### Ejemplos:

   10
   -10
   0.5
   -4.5
## Listas de argumentos
   Una lista de argumentos es el conjunto de valores que se pasan a una etiqueta de metadatos o a una propiedad. Si se pasan varios valores, se deben encerrar entre paréntesis. Si se pasa un solo valor, se omiten los paréntesis.

   Cada entrada dentro de la lista se llama argumento . Las tablas de referencia describen los parámetros correspondientes : las posiciones que el lenguaje acepta para una construcción dada.

## Un argumento puede ser:

   Un número entero: 3,-10
   Un número decimal: 3.3,-10.5
   Una cadena: "Hello",'Hello'
   Un identificador reservado: true, hide,x
   Ejemplos básicos:

   (1 2 3)— tres números
   ("Test" 3 hide)— tipos mixtos
   ### Ejemplos reales:
   \ts (3 4)— una indicación de compás de 3/4 en el alcance del compás
   12.2 { b (0 4 0) }— una flexión y liberación completas en una nota
   \title ("Song Title" "Title: %TITLE%" left)— un título de canción que se muestra como Title: Song Title, alineado a la izquierda
   Los argumentos se separan mediante espacios en blanco. No se utilizan comas.

## Propiedades
   Una propiedad es un name argumentspar de caracteres dentro de llaves. Las propiedades se adjuntan a los ritmos, las notas y las etiquetas de metadatos para agregar efectos, indicadores de visibilidad y otros aspectos opcionales.
   Los nombres de las propiedades no distinguen entre mayúsculas y minúsculas. La lista de argumentos de una propiedad sigue las reglas de Listas de argumentos .
```js
   \track "Track Name" { color "#FF0000" }
   \staff { score }
   C4 { b (0 4) v txt "Bend with Vibrato" }
```
## Etiquetas de metadatos
   Una etiqueta de metadatos es una construcción con prefijo de barra invertida de la forma \name arguments {properties}. Tanto la lista de argumentos como el bloque de propiedades son opcionales; las etiquetas individuales deciden qué argumentos y propiedades aceptan.

   Los nombres de las etiquetas de metadatos no distinguen entre mayúsculas y minúsculas.
```js
   \title "Song Title"
   \track "Track Name" { color '#FF0000' }
   \ts (3 4)
```
   Los argumentos de una etiqueta de metadatos siguen las listas de argumentos . Sus propiedades siguen las propiedades .

## Ámbitos
   Las construcciones de alphaTex se agrupan según su ubicación en el código fuente. Esta agrupación se denomina ámbito . Cada página de referencia de esta sección documenta un ámbito.

   A las etiquetas de metadatos se les aplican cuatro ámbitos:

## Metadatos estructurales
   Etiquetas que inician una nueva pista, personal o voz: \track, \staff, \voice. Documentado en metadatos estructurales .

## Metadatos de puntuación
   Etiquetas generales de la canción que describen la pieza: título, artista, tempo predeterminado, etc. Deben ubicarse al principio del archivo, encima del primer compás. Documentadas en Metadatos de la partitura .

## Metadatos del personal
   Etiquetas que configuran un pentagrama individual: su instrumento, afinación, tabla de articulación y ajustes relacionados. Documentado en Metadatos del pentagrama .

## Metadatos de la barra
   Etiquetas que se aplican a un solo compás: clave, armadura, compás, repeticiones. Documentadas en Metadatos del compás .

## A las propiedades se les aplican dos ámbitos:
### Propiedad Beat
   Una propiedad asociada a un compás, que controla los efectos o anotaciones que se aplican a cada nota de ese compás. Documentada en Propiedades del compás .
### Propiedad de la nota
   Una propiedad asociada a una sola nota, que controla los efectos específicos de esa nota. Documentada en Propiedades de la nota .
## Firmas y sobrecargas
   Cada entrada de referencia incluye una o más firmas . Una firma es una lista de parámetros aceptada para la construcción: los parámetros que nombra, sus tipos y su orden. Al escribir una etiqueta de metadatos o una propiedad, la lista de argumentos debe coincidir exactamente con una de sus firmas.

   Una construcción con más de una firma se sobrecarga . \titlePor ejemplo, acepta una sola cadena en una firma y una tripleta de título, plantilla y alineación en otra. La página de referencia de cada construcción muestra todas las firmas que acepta.

## Distinción entre mayúsculas y minúsculas
   Los nombres de las etiquetas de metadatos, los nombres de las propiedades y los identificadores reservados, como true, hide, y , xno distinguen entre mayúsculas y minúsculas. \Title, \title, y \TITLEtodos se analizan de la misma manera.

   El contenido de los literales de cadena distingue entre mayúsculas y minúsculas. Lo mismo ocurre con la letra de tono de una nota afinada: C4y c4son notas diferentes. Las alteraciones utilizan el formato que se muestra en Notas afinadas ( #, b, bb, x, ##).

## Espacio en blanco
   Los espacios en blanco entre tokens no son relevantes. Los saltos de línea, las tabulaciones y las secuencias de espacios separan los tokens por igual. Utilice los espacios en blanco libremente para facilitar la lectura del código fuente.

   No se permiten espacios en blanco dentro de un mismo valor. La notación de notas en traste debe escribirse fret.stringsin espacio alrededor del punto, y el valor de una nota afinada debe escribirse como tono-octava-accidente sin espacio entre las partes.

   ## Notación de traste
   En un instrumento de cuerda, una nota se escribe como fret.string. El número antes del punto indica el traste. El número después del punto indica la cuerda, contada desde la más aguda hacia abajo. La cuerda 1 es la cuerda superior al leer la tablatura; es la más delgada de la guitarra y, por lo tanto, la que produce el sonido más agudo.
```js
   5.6      // fret 5 on string 6 (the lowest string on a 6-string guitar)
   0.1      // an open note on string 1 (the highest string)
   12.3     // fret 12 on string 3
```
   Un acorde de sol mayor en afinación estándar hace vibrar seis cuerdas a la vez:
```js
   (3.6 2.5 0.4 0.3 0.2 3.1).4
```
   El acorde completo se escribe como un pulso entre paréntesis porque seis notas resuenan simultáneamente. Consulta las listas de argumentos para conocer las reglas de los paréntesis.

## Ejemplo de partitura
```js
/* =========================================================
   METADATOS GLOBALES DE LA PARTITURA
   ========================================================= */
\title "Demo Completa de Efectos AlphaTex"
\subtitle "Muestrario exhaustivo de técnicas y metadatos en 4/4"
\tempo 100
.

/* =========================================================
   PISTA 1: GUITARRA LÍDER (15 compases en 4/4)
   ========================================================= */
\track "Guitarra Líder" "Gtr."
\instrument 25 // MIDI 25 (base 0) = Guitarra Acústica Cuerdas de Acero
\tuning E4 B3 G3 D3 A2 E2 // Afinación estándar de 1ª a 6ª cuerda (sin paréntesis)
\chord "Am" 0 1 2 2 0 x // Diagrama de acorde (trastes de 1ª a 6ª cuerda)

// Compás 1: Ligados — Hammer-on (ascendente) y Pull-off (descendente)
\ts 4 4
\ks C
\section "A" "Ligados y Slides"
:4 5.2{h} 7.2 8.2{h} 5.2 | // h: hammer-on (5->7) y pull-off (8->5)

// Compás 2: Slides entre notas en la misma cuerda
:4 5.2{sl} 7.2 7.2{ss} 10.2 | // sl = legato slide (sin repulsar), ss = shift slide (repulsando destino)

// Compás 3: Entradas y salidas con slide
:4 7.1{sib} 7.1{sia} 7.1{sod} 7.1{sou} | // sib/sia = slide in below/above, sod/sou = slide out down/up

// Compás 4: Bends (automático y exacto) y ligadura de prolongación (tie)
// Valores en cuartos de tono: 2 = 1/2 tono, 4 = 1 tono. Offset de "be": 0 a 60.
:4 7.2{b (0 4 0)} 8.2{be (0 0 30 2 60 2)} 8.2 -.2 | // -.2 liga la nota en la 2ª cuerda

// Compás 5: Armónicos (5 tipos: 3 negras + 2 corcheas = 4 tiempos)
:4 12.1{nh} 5.2{ah} 5.2{th} :8 7.3{ph} 7.3{sh} | // nh = natural, ah = artificial, th = tapped, ph = pinch, sh = semi

// Compás 6: Muteos, nota fantasma, dead note y let ring
:4 5.2{g} x.3 0.6{pm} 3.1{lr} | // g = ghost note, x.3 = dead note, pm = palm mute, lr = let ring

// Compás 7: Articulaciones y trino
:4 5.1{st} 5.1{ac} 5.1{hac} 5.1{tr 7 16} | // st = staccato, ac = acento, hac = marcato, tr = trino a traste 7 en 16avos

// Compás 8: Vibrato y palanca de trémolo (automática y exacta)
:4 7.2{v} 7.2{vw} 5.2{tb (0 -4 0)} 5.2{tbe (0 0 30 -2 60 0)} | // v/vw = vibrato leve/amplio, tb/tbe = whammy bar

// Compás 9: Envolventes de volumen y dinámica puntual
:4 5.2{f} 5.2{fo} 5.2{vs} 5.1{dy ff} | // f = fade in, fo = fade out, vs = volume swell, dy = dinámica (ppp..fff)

// Compás 10: Crescendo, decrescendo y tremolo picking
:4 5.1{dy p cre} 6.1{cre} 7.1{dy ff dec} 5.1{tp 16 dec} | // cre/dec = reguladores, tp 16 = tremolo picking en 16avos

// Compás 11: Rasgueos (brush) y arpegios sobre tríada de Am
:4 (0.1 1.2 2.3){bu} (0.1 1.2 2.3){bd} (0.1 1.2 2.3){au} (0.1 1.2 2.3){ad} | // bu/bd = brush up/down, au/ad = arpeggio up/down

// Compás 12: Dirección de púa, tapping y apoyaturas (las grace notes duran 0 tiempos)
:4 5.6{sd} 5.6{su} 10.1{gr} 12.1{tt} 5.1{gr ob} 7.1 | // sd/su = púa abajo/arriba, tt = tapping, gr / gr ob = grace before/on beat

// Compás 13: Puntillos (1.5 + 0.5 + 1.75 + 0.25 = 4 tiempos), digitación y alteraciones
// Digitación lf/rf: 1=pulgar, 2=índice, 3=medio, 4=anular, 5=meñique
:4 5.1{d lf 2 rf 2} :8 6.1{acc forceSharp lf 3 rf 3} :4 7.1{dd lf 4 rf 4} :16 8.1{lf 5 rf 2} |

// Compás 14: Repetición de compás, cambio de tempo y líneas de octava
\section "B" "Repetición y Octavas"
\ro \rc 2 \tempo 110
:4 5.1{ot 8va} 7.1{ot 8va} 5.6{ot 8vb} 3.6{ot 8vb} | // \ro/\rc 2 = barra de repetición (x2), ot = 8va alta / 8vb baja

// Compás 15: Tresillo (1t) + texto (1t) + acorde arpegiado con cifrado y calderón (2t) + doble barra
\section "C" "Final"
\tempo 100
\db
:8 5.1{tu 3} 6.1{tu 3} 7.1{tu 3} :4 5.1{txt "Final"} :2 (0.1 1.2 2.3 2.4 0.5){ch "Am" ad fermata medium} |

/* =========================================================
   PISTA 2: BAJO ELÉCTRICO (15 compases sincronizados)
   ========================================================= */
\track "Bajo Demo" "Bajo"
\instrument 33 // MIDI 33 (base 0) = Bajo Eléctrico (Finger)
\tuning G2 D2 A1 E1 // Afinación estándar 4 cuerdas (sin paréntesis)
\clef F4 // Clave de Fa en 4ª línea

// Compás 1: Slap, Pop, Dead Slap y silencio de negra (4 tiempos)
:4 3.4{s} 5.1{p} x.4{ds} r | // s = slap, p = pop, ds = dead slapped, r = silencio

// Compases 2 a 14: Silencios de compás completo (13 compases)
r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 | r.1 |

// Compás 15: Tónica final acompañando el acorde de Am (el calderón es global del compás)
:2 r :2 0.3{dy ff} | // 0.3 = La al aire (A1) en 3ª cuerda
```