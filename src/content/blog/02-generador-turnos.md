---
title: 'El programa que mis compañeros no quisieron usar'
description: 'Construí un generador automático de turnos médicos con Claude. Lo rechazaron. Lo terminé igual. Y eso cambió algo.'
pubDate: '2026-05-10'
tags: ['python', 'medicina', 'herramientas']
heroImage: '../../assets/banner-turnos.png'
---

Yo no era el encargado de hacer el cuadro de guardias. Ese era el problema de otro. Pero cuando tienes Claude y ves a tus compañeros peleando cada mes con ChatGPT para cuadrar los turnos de diez médicos, algo dentro de ti dice: *jumm, y si les echo una mano.*

Así que se lo propuse a la persona que llevaba eso. En vez de usar ChatGPT cada vez que había que hacer un cuadro nuevo, ¿por qué no un software que lo hiciera automáticamente? Unos cuantos clics y listo. Ellos no lo vieron viable.

Yo sí. Y lo hice igual, por puro amor al arte.

---

## La idea

El problema de cuadrar guardias médicas parece simple hasta que te sientas a pensarlo. No es solo "a quién le toca hoy". Hay condiciones que respetar:

- Descanso obligatorio de 48 horas después de cada guardia
- Guardias diurnas (08:00–22:00) cubiertas por 2 médicos
- Guardias nocturnas (22:00–08:00) cubiertas por 1 médico
- Tener en cuenta la carga del mes anterior para no sobrecargar siempre a los mismos
- Recordar quién hizo la última y penúltima guardia del mes anterior, para aplicar el descanso de 48h desde el inicio del mes nuevo
- Permitir marcar vacaciones por rangos de fechas
- Permitir marcar días en los que un médico prefiere no tener guardia

Hacer eso a mano, o pidiéndoselo a ChatGPT cada mes, es trabajo. Mi propuesta era automatizarlo de una vez.

---

## Cómo lo construí con Claude

Lo primero que aprendí con el cortador de PDFs fue que lanzarse sin pensar es perder tiempo y tokens. Así que antes de escribir una sola línea de prompt, me senté a diseñar el programa en la cabeza. ¿Qué tiene que hacer exactamente? ¿Qué datos necesita? ¿Cómo quiero que se vea el resultado?

Mi recomendación para cualquiera que quiera hacer algo parecido: **diseñen primero en papel**. Escriban qué cosas le pondrían al programa, cómo funcionaría, qué botones tendría. Cuando llegue el momento de hablar con Claude, solo es dar directrices claras y en bloque. Se ahorran mucho tiempo y muchas vueltas.

Con eso claro, tuve una conversación larga con Claude sobre las condiciones del cuadro, el diseño de la interfaz y cómo quería que se generara el resultado. Fue un proceso de prueba y error, con paciencia. No es escribir un prompt y llegar inmediatamente al resultado deseado.

El primer resultado que me dio funcionaba... pero mal. Las guardias no salían en formato de cuadrícula mensual sino como una línea temporal. Útil quizás, pero no era lo que yo tenía en mente. Así que seguimos. Ajustes, pruebas, más ajustes.

En ningún momento pensé "esto no va a funcionar". Me dije: si no funciona así, busco la manera. Algo ha de funcionar.

Y funcionó.

Una cosa que me inventé en el proceso y de la que estoy especialmente orgulloso: **el sistema de semilla**, inspirado directamente en Minecraft. Para los que no lo saben, en Minecraft cada mundo se genera a partir de una serie de números llamada semilla — cada semilla produce un mundo completamente diferente pero siempre reproducible. Tomé ese concepto y lo apliqué a la generación de turnos. Si el cuadro generado no convencía a alguien, bastaba con cambiar el número de semilla y darle al botón para obtener una distribución completamente distinta, respetando todas las condiciones. Sin tocar nada más.

---

## El resultado

El programa tiene una interfaz gráfica donde configuras todo antes de generar:

- El mes y año del cuadro
- Los parámetros: máximo de horas al mes, máximo de noches por semana, días de descanso, semilla
- La lista de médicos
- Las vacaciones de cada uno, por rangos de fechas
- Las peticiones de días libres (no obligatorias, máximo 5 por médico)
- El historial de horas del mes anterior, para el balanceo

![Interfaz del Generador de Turnos](/generador-turnos-ui.jpg)

Le das al botón de generar y el programa produce un PDF con dos páginas: el cuadro mensual en formato cuadrícula, con cada día mostrando quién hace la guardia diurna y quién la nocturna, y las vacaciones marcadas; y una segunda página con la carga horaria de cada médico en ese mes.

![Cuadrante de turnos generado](/cuadrante-turnos.jpg)

En el ejemplo de arriba, el Médico 6 está de vacaciones del 1 al 15 de junio y el Médico 5 del 15 al 30. El programa lo respeta automáticamente sin que tengas que hacer nada más.

---

## Lo que aprendí

Cuando el cuadro de guardias apareció por primera vez en formato de cuadrícula, bien distribuido, respetando todas las condiciones, me sentí muy bien conmigo mismo. Pero no fue cantar victoria total — fue ganar una batalla, porque todavía quedaba trabajo por hacer.

Lo que sí fue diferente a todo lo anterior fue la reacción de mis compañeros. O más bien, la ausencia de reacción. Decidieron seguir con ChatGPT. No sé las razones y ya no me interesan. En su momento me sentí ignorado, como si el trabajo no valiera nada.

Pero no lo tomé como una derrota.

Creo que fue ahí, en ese momento, donde tomé la decisión de hacer este blog. Si mis compañeros no iban a ver lo que estaba construyendo, pues que lo viera quien quisiera. Que quedara documentado. Que sirviera de algo.

Así que en cierta forma, el rechazo de ese cuadro de guardias es la razón de que este blog exista.

---

*¿Quieres construir algo con Claude sin saber programar? Mi consejo más útil: diseña primero en papel, habla con Claude después. La claridad de lo que quieres es la mitad del trabajo.*
