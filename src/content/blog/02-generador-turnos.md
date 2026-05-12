---
title: 'El programa que sigo mejorando'
description: 'Cómo construí con Claude un generador automático de cuadros de guardias médicas'
pubDate: '2026-05-10'
tags: ['python', 'medicina', 'herramientas']
heroImage: '../../assets/banner-turnos.png'
---

Yo no era el encargado de hacer el cuadro de guardias. Ese era el problema de otro. Pero cuando tienes Claude y ves a tus compañeros peleando cada mes con ChatGPT para cuadrar los turnos de diez médicos, algo dentro de ti dice: jumm, ¿y si lo automatizamos de verdad?

Así que lo hice. Por puro amor al arte.

## La idea

El problema de cuadrar guardias médicas parece simple hasta que te sientas a pensarlo. No es solo "a quién le toca hoy". Hay condiciones que respetar:

- Descanso obligatorio de 48 horas después de cada guardia
- Guardias diurnas (08:00–22:00) cubiertas por 2 médicos
- Guardias nocturnas (22:00–08:00) cubiertas por 1 médico
- Tener en cuenta la carga del mes anterior para no sobrecargar siempre a los mismos
- Recordar quién hizo la última y penúltima guardia del mes anterior, para aplicar el descanso de 48h desde el inicio del mes nuevo
- Permitir marcar vacaciones por rangos de fechas
- Permitir marcar días en los que un médico prefiere no tener guardia

Hacer eso a mano cada mes es trabajo. Mi propuesta era automatizarlo de una vez.

## Cómo lo construí con Claude

Lo primero que aprendí con el cortador de PDFs fue que lanzarse sin pensar es perder tiempo y tokens. Así que antes de escribir una sola línea de prompt, me senté a diseñar el programa en la cabeza. ¿Qué tiene que hacer exactamente? ¿Qué datos necesita? ¿Cómo quiero que se vea el resultado?

Mi recomendación para cualquiera que quiera hacer algo parecido: diseñen primero en papel. Escriban qué cosas le pondrían al programa, cómo funcionaría, qué botones tendría. Cuando llegue el momento de hablar con Claude, solo es dar directrices claras y en bloque. Se ahorran mucho tiempo y muchas vueltas.

Con eso claro, tuve una conversación larga con Claude sobre las condiciones del cuadro, el diseño de la interfaz y cómo quería que se generara el resultado. El primer resultado funcionaba… pero mal. Las guardias no salían en formato de cuadrícula mensual sino como una línea temporal. Útil quizás, pero no era lo que yo tenía en mente. Así que seguimos. Ajustes, pruebas, más ajustes.

En ningún momento pensé "esto no va a funcionar". Me dije: si no funciona así, busco la manera. Algo ha de funcionar.

Y funcionó.

Una cosa que me inventé en el proceso y de la que estoy especialmente orgulloso: el sistema de semilla, inspirado directamente en Minecraft. Para los que no lo saben, en Minecraft cada mundo se genera a partir de una serie de números llamada semilla — cada semilla produce un mundo completamente diferente pero siempre reproducible. Tomé ese concepto y lo apliqué a la generación de turnos. Si el cuadro generado no convencía, bastaba con cambiar el número de semilla y darle al botón para obtener una distribución completamente distinta, respetando todas las condiciones. Sin tocar nada más.

## El resultado: v1

El programa tenía una interfaz gráfica donde configurabas todo antes de generar: el mes y año, los parámetros, la lista de médicos, las vacaciones, las peticiones de días libres y el historial de horas del mes anterior. Le dabas al botón y producía un PDF con el cuadro mensual en formato cuadrícula y una segunda página con la carga horaria de cada médico.

<img src="/generador-turnos-ui.jpg" alt="Interfaz del Generador de Turnos v1" style="width: 80%; display: block; margin: 0 auto;" />

Funcional. Pero todo en vertical, había que hacer bastante scroll para llegar al botón de generar, y cada vez que cerrabas el programa tenías que volver a escribir todo desde cero.

Cuando el cuadro apareció por primera vez bien distribuido, respetando todas las condiciones, me sentí muy bien conmigo mismo. Pero no fue cantar victoria total — fue ganar una batalla, porque todavía quedaba trabajo por hacer.

El cuadro que genera el programa se ve así:

<img src="/cuadrante-turnos.jpg" alt="Cuadrante de turnos generado" style="width: 80%; display: block; margin: 0 auto;" />

En el ejemplo, el Médico 6 está de vacaciones del 1 al 15 de junio y el Médico 5 del 15 al 30. El programa lo respeta automáticamente sin que tengas que hacer nada más.

## Las mejoras: v5

Tiempo después volví al programa. El código había crecido de forma un poco caótica — lo típico cuando vas añadiendo cosas sobre la marcha — así que lo primero fue pedirle a Claude Opus que lo reorganizara. Nada de funcionalidades nuevas todavía, solo limpiar la casa. El resultado fue un código mucho más ordenado, más fácil de leer y de modificar.

Con esa base sólida, vinieron las mejoras de verdad. La más visible: la interfaz.

<img src="/generador-turnos-ui-v5.jpg" alt="Interfaz del Generador de Turnos v5" style="width: 80%; display: block; margin: 0 auto;" />

Antes todo iba en una sola columna vertical. Ahora los elementos están distribuidos en dos columnas, el botón de generar siempre está visible sin hacer scroll, y la ventana no tiene espacios muertos. Se ve más limpio y se usa mejor.

Además de la interfaz, vinieron estas mejoras:

- **Barras de desplazamiento con rueda del ratón:** las listas de médicos y peticiones ahora se desplazan de forma natural.
- **Memoria entre sesiones:** la información que introduces — médicos, vacaciones, parámetros — se guarda y vuelve a aparecer la próxima vez que abres el programa. Sin tener que volver a escribirlo todo.
- **Cálculo de horas anuales:** el programa ahora tiene en cuenta las horas totales que debe cumplir cada médico en el año, descontando vacaciones, y distribuye en consecuencia.

## Lo que aprendí

La v1 funcionaba. Pero la v5 es mejor — más limpia, más cómoda, más pensada. Y habrá una v6, probablemente.

Eso es lo que más me gusta de construir cosas así: no hay un punto de llegada definitivo. Siempre hay algo que mejorar, algo que no habías pensado, algo que se te ocurre cuando ya lo estás usando. El programa no lo usa nadie más que yo, y aun así le sigo dedicando tiempo. Porque me gusta construir. Y me gusta documentar lo que construyo.

Si quieres hacer algo parecido con Claude sin saber programar: diseña primero en papel, habla con Claude después. La claridad de lo que quieres es la mitad del trabajo.
