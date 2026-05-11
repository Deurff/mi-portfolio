---
title: 'Construí mi primer programa y no sé cómo funciona del todo'
description: 'Cómo le pedí a Claude que me hiciera un cortador de PDFs desde cero, sin saber programar, y por qué eso me cambió algo por dentro.'
pubDate: '2026-05-11'
tags: ['python', 'herramientas', 'primer-proyecto']
heroImage: '../../assets/banner-pdf.png'
---

Hay una versión de mí de hace unos meses que aún usaba ilovepdf para todo. Subía el PDF, esperaba que cargara, seleccionaba las páginas, descargaba, volvía a subir para el siguiente fragmento... y así una y otra vez. Con conexión a internet. Con la paciencia de un santo.

El problema era concreto: yo necesitaba cortar varios fragmentos de un PDF al mismo tiempo. No uno detrás de otro. Varios, de golpe, con los nombres que yo quisiera y guardados donde yo quisiera. Eso ilovepdf no lo hace. Y yo no iba a pagar por algo que debería ser simple.

Entonces me acordé de que tenía Claude.

---

## La idea

La conversación interna fue más o menos así: *"Vale Juan, dicen que esto es una pasada. Pues a ver si es verdad."*

No tenía ni idea de por dónde empezar. Ni lenguaje, ni librerías, ni nada. Solo sabía lo que quería que hiciera el programa: seleccionas un PDF, le dices qué páginas quieres en cada fragmento, le pones nombre a cada uno, y listo. Sin terminal. Sin comandos raros. Como un programa normal.

Se lo expliqué a Claude exactamente así, en lenguaje de persona que no sabe programar. Y empezamos.

---

## Cómo lo construí con Claude

El proceso fue en bloques. Yo le daba una indicación general de lo que quería, él me pedía más detalles o me hacía preguntas para ir afinando, y con cada intercambio la cosa tomaba forma.

Lo que más me sorprendió fue esto: cada vez que aparecía algo que yo no entendía —que era constantemente— le preguntaba, y él me lo explicaba. Sin hacerme sentir tonto. Sin saltarse pasos. Así fui construyendo lo que llamo un "mapa mental" de lo que estaba pasando: no entiendo el código línea por línea, pero sé qué hace cada parte y por qué existe.

El resultado es esto:

<img src="/src/assets/divisor-pdf-ui.jpg" alt="Interfaz del Divisor de PDF" style="width: 50%; display: block; margin: 0 auto;" />

Una ventana con tres zonas:

1. **PDF de entrada**: seleccionas el archivo que quieres cortar.
2. **Carpeta de salida**: le dices dónde guardar los fragmentos.
3. **Documentos a generar**: una tabla donde añades tantas filas como quieras. Cada fila es un fragmento: le pones nombre, página de inicio y página final.

Le das a "Dividir PDF" y listo. Todos los fragmentos aparecen en la carpeta, con sus nombres, en segundos. Sin internet. Sin páginas de terceros. Sin repetir el proceso diez veces.

¿Es bonita la interfaz? Nel, para nada. Parece de los años 90 y yo lo sé perfectamente. Pero es mía, funciona exactamente como yo necesitaba, y no le quema el computador a nadie. Para uso personal, eso es todo lo que importa.

---

## Lo que aprendí

Siendo honesto: como fue mi primer proyecto, ya no recuerdo con precisión cada cosa que aprendí técnicamente. El tiempo hace eso.

Pero sí recuerdo lo que sentí cuando el programa funcionó por primera vez.

Para cualquier desarrollador junior serio —no como yo, que lo he hecho a punta de trampas— esto es una tontería. Un ejercicio de tarde. Algo que harían con los ojos cerrados.

Pero para mí fue otra cosa. Fue darme cuenta de que podía construir algo que no existía y que resolvía un problema real mío. Que no tenía que esperar a saber programar "de verdad" para empezar. Que la barrera de entrada ya no era la misma de antes.

Aquello activó algo. Como cuando enciendes un motor que llevaba tiempo parado y escuchas que arranca. Eso fue lo que pasó.

Y desde ahí vinieron todos los demás proyectos.

---

*Hablando de gente que sí sabe programar de verdad: mi amigo [Fabián Enrique Gutiérrez](https://fega.github.io/) es desarrollador senior y aprendió sin la ayuda de la IA. Su portafolio es una pasada, dadle un vistazo.*
