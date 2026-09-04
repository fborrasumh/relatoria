# RelatorIA

De la grabación de una clase a dos documentos distintos: el **cuaderno docente** que el
profesor publica y los **apuntes de estudio** que el estudiante necesita. No son lo mismo,
y de la misma transcripción salen los dos.

Con Chrome, la transcripción ocurre en el propio equipo: el audio no sale del ordenador
y no cuesta nada.

**Aplicación**: https://fborrasumh.github.io/relatoria/

## El recorrido

1. **Quién eres y en qué idioma.** El perfil decide el resultado. Treinta y dos idiomas.
2. **La grabación.** Sube audio o vídeo, o graba desde el micrófono si estás en clase.
   De un vídeo se extrae solo la pista de audio.
3. **La transcripción.** Tres motores, elegidos según disponibilidad.
4. **El cuaderno.** Cada sección lleva el minuto de la grabación donde se explicó, para
   poder volver a escucharlo.

## Los tres motores

| Motor | Coste | Privacidad | Requisitos |
|---|---|---|---|
| Chrome local (`processLocally`) | ninguno | el audio no sale del equipo | Chrome o Edge 139+, paquete del idioma |
| Chrome remoto | ninguno | el audio va a los servidores del navegador | Chrome o Edge |
| Whisper | ~0,30 $ por 50 min | el audio va a OpenAI | clave de OpenAI |

Los dos motores de Chrome escuchan en tiempo real: una clase de cincuenta minutos tarda
cincuenta minutos a 1x. El selector de velocidad acorta la espera a cambio de precisión;
2x es un equilibrio razonable, 3x pierde palabras. Whisper no depende de la velocidad:
trocea el audio en fragmentos de diez minutos (19 MB en WAV a 16 kHz, por debajo del
límite de 25 MB) y devuelve las marcas de tiempo más exactas de los tres.

La API de voz de Chrome no da marcas de tiempo. RelatorIA las reconstruye anotando la
posición de reproducción cada vez que llega un fragmento reconocido, así que son
aproximadas; las de Whisper vienen del propio modelo y son fiables.

## Las dos salidas

**Cuaderno docente**: de qué fue la clase, objetivos deducidos de lo explicado, desarrollo
por secciones con su minuto, las preguntas que salieron en clase con su respuesta,
ejercicios, glosario, lo que quedó pendiente y los avisos con fecha.

**Apuntes de estudio**: qué repasar antes, los apuntes con sus minutos, las fechas y avisos,
las dudas que quedaron en el aire, ocho preguntas de autoevaluación con la respuesta
plegada, y una sección que no tiene equivalente en el material oficial: **lo que el profesor
dijo de viva voz** y no está escrito en ninguna parte —los matices, las advertencias, cómo
quiere que se resuelva algo—. Es la razón de ser de la salida del estudiante.

En ambas, lo que no se entiende se marca como tal en vez de completarse, y las cifras o
nombres dudosos llevan un `(?)`.

## Grabar una clase

En una grabación de aula se oye al profesor y a veces a los compañeros. Que el motor local
no envíe el audio a ningún sitio y que RelatorIA no guarde nada en ningún servidor hace la
herramienta defendible, pero no sustituye al permiso de quien imparte la clase. La app lo
dice en su propia interfaz.

## Navegadores

El reconocimiento de voz llegó en Chrome y Edge 139; Firefox y Safari no lo tienen. En esos
navegadores queda la ruta de Whisper, que funciona en todos. La disponibilidad del motor
local depende del idioma y puede requerir descargar una vez el paquete de voz.

## Licencia

CC BY-SA 4.0.
