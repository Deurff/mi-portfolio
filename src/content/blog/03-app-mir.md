---
title: 'AutoMIR: la app que Miguel y yo construimos para estudiar'
description: 'Cómo pasamos de hacer resúmenes a mano en NotebookLM a tener un programa que los hace solo, usando la API de Claude'
pubDate: '2026-05-12'
tags: ['claude-api', 'medicina', 'mir', 'python']
heroImage: '../../assets/banner-mir.png'
---

El año pasado empecé a estudiar para el MIR con una de las muchas academias de preparación que hay. Para no quedarme atrás me compré una tablet — vi a mi amigo Miguel con la suya y un Apple Pencil tomando resúmenes a una velocidad que me daba envidia. El salto fue significativo: pasar del papel a la tinta digital, ver tu propia caligrafía en pantalla, tener todo organizado en un solo dispositivo. Adiós lápiz y papel.

Le dedicaba horas a las videoclases del día y a enriquecerlas con los temas del manual. Estudiaba mucho. Y aun así, a veces no era capaz de cubrir todos los temas del día. Estudiaba pero no repasaba. Me sentía frustrado.

Hasta que vi a Miguel usando algo que en su momento me pareció trampa.

## El click

Era una guardia tranquila, sin pacientes llegando. Me asomé al consultorio donde estaba Miguel.

> **Yo:** Hey, ¿qué hace?
> **Él:** Aquí, haciendo los resúmenes de la semana.
> **Yo:** ¿Khé? ¿Cómo así?
> **Él:** Sí, le digo a NotebookLM que tome la transcripción de la clase y la enriquezca con el contenido del capítulo del manual. Luego pongo la videoclase y agrego lo que falte.

Ahí algo hizo CLICK. Me pareció que era estudiar impulsado por un cohete.

Miguel me enseñó que había que darle a NotebookLM un prompt específico, hacerlo actuar como un entrenador experto en materias del MIR, pidiéndole que generara resúmenes eficientes haciendo hincapié en los temas que más caen. Le copié la idea, monté mi primer prompt y le di a procesar.

Cuando vi cómo integraba conceptos de la transcripción con el manual quedé asombrado. Era pasar del caballo a la locomotora.

Pero rápido aparecieron los problemas.

NotebookLM omitía fragmentos enteros de la clase. Y eso no me servía, porque el objetivo era ahorrar tiempo, no añadir una tecnología por añadirla. Intenté pedirle que entregara los resúmenes en paquetes — varios outputs, cada uno desarrollando una parte del tema. Mejoró, pero seguía dejándose cosas por el camino. Y el tiempo que me ahorraba integrando información, lo gastaba metiendo a mano lo que NotebookLM había olvidado.

## El siguiente paso: Claude

Un día se me ocurrió: ¿y si uso Claude para esto? Ya pagaba el plan Pro y había visto lo que era capaz de hacer Opus.

Le metí el mismo prompt que le daba a NotebookLM, subí el PDF de la transcripción y el del capítulo de refuerzo, y… vualá. Todo quedaba **perfecto**. La transcripción servía como esqueleto del documento final — la guía temática cronológica — y Claude la respetaba íntegra. Eliminaba redundancias y añadía dos o tres puntos de refuerzo por epígrafe, decidiendo cuáles según lo rentable que fuera el tema para el examen.

Pero quedaba un problema: la automatización. Claude generaba la respuesta en varios fragmentos y tocaba ir dándole "continuar" cada vez. Eso, **si fuera un solo tema**, no sería molestia. El problema es que una semana cualquiera son 14 temas. Y darle continuar 14 veces, copiar, pegar, organizar archivos… eso ya es trabajo.

## La noche de las empanadas

Por esa época empecé a notar algo curioso: desde que me había metido a hacer cosas con Claude, mi algoritmo de TikTok había cambiado por completo. Donde antes salían recetas y memes ahora salían vídeos sobre IA y desarrollo. En uno de esos vídeos escuché por primera vez algo llamado **la API de Claude**. Qué interesante, pensé.

Para que se entienda, una explicación rápida: el Claude que usamos a diario (la web o la app de escritorio) es como un trabajador al que le hablas escribiendo. La API es el mismo Claude pero al que puedes llamar desde tu propio programa. En vez de yo escribirle "hazme el resumen de hepatitis", mi programa le manda los PDFs automáticamente y recibe la respuesta sin que yo tenga que estar dándole continuar.

La pega: la API es algo **aparte** del plan Pro o Max. Aunque ya pagues la suscripción mensual de Claude, para usar la API tienes que recargarle tokens a una cuenta distinta. Los tokens son como su salario — vas gastando según el trabajo que le pidas. Yo no quería gastar más en IA, así que seguía haciendo los resúmenes a mano.

Hasta que una noche invitamos a Miguel a comer empanadas colombianas en casa. Le mostré cómo hacía Claude los resúmenes y le mencioné que existía una forma mucho más automática, pero que estaba la limitación del dinero.

Para él no fue una limitación.

> **Miguel:** Pues Juanito, metámosle 50 dólares a eso y que nos haga los resúmenes. Es capaz de hacer el programa?
> **Yo:** Sí, eso es solo coordinar a Claude para que lo haga.
> **Él:** Pues hagámosle, ¿qué carajos?

Esa noche metimos 25 dólares cada uno. La API quedó recargada. Empezó la fase de desarrollo.

## Construyendo AutoMIR

Le contamos a Claude (modo Opus pensante) lo que queríamos hacer. Nos hizo preguntas para afinar los detalles y arrancó. En **dos o tres horas** teníamos un programa funcional que hacía todo automáticamente. Incluso al final de cada documento generado nos decía cuántos dólares de tokens había gastado en ese tema. Era revolucionario.

El nombre del programa, **AutoMIR**, lo propuso Claude. A los dos nos gustó y se quedó. Jajaja.

En esa primera versión todo funcionaba por terminal — ventana negra, comandos, sin botones. Funcionaba, pero no era cómodo. Así que tocaba interfaz gráfica. Y aquí apliqué lo que aprendí con el generador de turnos: antes de hablar con Claude, pensar. ¿Qué funciones quiero que se vean? ¿Cómo se organizan las pestañas? ¿Qué tiene que pasar al pulsar cada botón? Cuando piensas antes de actuar, quedan cosas bonitas.

## El Clasificador (un paso previo necesario)

Antes de mostrar AutoMIR tengo que hablar de un programa hermano: el **Clasificador**.

¿Por qué hizo falta? Porque para que AutoMIR funcione necesita saber qué transcripción va con qué capítulo del manual. Y los nombres originales de los archivos no le ayudaban a inferirlo. Por ejemplo:

- `Osteoporosis_transcripcion_academiaMIR.pdf`
- `Capitulo osteoporosis manual.pdf`

Tienen nombres muy distintos. Para que el programa los empareje hace falta un criterio común. Si fuera un tema bastaría con renombrarlos a mano, pero **14 temas son 28 archivos**. La solución fue otro programa que se encarga solo de eso. Nombre supercreativo: Clasificador.

Funciona así. Cuando arrancas el Clasificador y aún no hay nada en la carpeta, la interfaz está vacía:

<img src="/Clasificador1.jpg" alt="Interfaz del Clasificador vacía" style="width: 80%; display: block; margin: 0 auto;" />

Apenas meto un par de PDFs en la carpeta que vigila, aparece este diálogo:

<img src="/Clasificador2.jpg" alt="Clasificador detectando un archivo nuevo" style="width: 65%; display: block; margin: 0 auto;" />

Arriba se ve el nombre original del archivo: `Hepatitis_agudas_virales_academiaMIR.pdf`. El programa me pregunta qué tipo de documento es: **BASE** (la transcripción) o **REFUERZO** (el capítulo del manual). En este caso es la transcripción, así que marco BASE:

<img src="/Clasificador3.jpg" alt="Marcando el archivo como BASE" style="width: 65%; display: block; margin: 0 auto;" />

El programa me sugiere un nombre limpio para el archivo resultante: `Hepatitis_agudas_virales_academia`. Lo puedo editar — lo dejo como `Hepatitis_agudas_virales` y guardo.

Cuando aparece el segundo archivo (el de refuerzo), marco REFUERZO y selecciono de la lista el documento BASE con el que se debe emparejar:

<img src="/Clasificador4.jpg" alt="Emparejando refuerzo con base" style="width: 65%; display: block; margin: 0 auto;" />

<img src="/Clasificador5.jpg" alt="Par completo listo para procesar" style="width: 65%; display: block; margin: 0 auto;" />

Y ya está. El par queda guardado con nombres que AutoMIR puede entender.

## Cómo funciona AutoMIR

Ahora sí, el programa principal. Tiene cinco pestañas: Procesar, Resultados, Flashcards, Enviar y Ajustes.

**Procesar** es donde empieza todo. Aparece la lista de pares que el Clasificador ha dejado listos. En este ejemplo se ve el par de Hepatitis virales agudas — el programa ya sabe que la base y el refuerzo son el mismo tema, así que no aparecen como dos elementos sino como uno solo:

<img src="/Interfaz1.jpg" alt="AutoMIR — pestaña Procesar" style="width: 90%; display: block; margin: 0 auto;" />

Le doy a procesar y en el recuadro negro de la derecha aparece el log del proceso, parecido a la consola de Windows. Veo cómo Claude va integrando los documentos en tiempo real.

**Resultados** es donde aparecen todos los documentos ya procesados, listos como archivos Word. Puedo abrir cualquiera con un clic o marcar varios para enviarlos:

<img src="/Interfaz2.jpg" alt="AutoMIR — pestaña Resultados" style="width: 90%; display: block; margin: 0 auto;" />

**Enviar** es la pestaña a la que salta el programa cuando marco documentos para enviar por correo. Solo escribo el destinatario, el programa ya trae un asunto y un cuerpo prediseñados. Tengo una dirección guardada como favorita — la de Miguel, claro:

<img src="/Interfaz3.jpg" alt="AutoMIR — pestaña Enviar" style="width: 90%; display: block; margin: 0 auto;" />

**Flashcards** fue lo último que se le añadió al programa. La idea salió esa misma noche de las empanadas, pero la implementación fue días después. Selecciono uno o varios documentos procesados y el programa, mediante un prompt interno, genera 70-100 flashcards eficientes del tema y las exporta en un formato que se importa directamente a Anki:

<img src="/Interfaz4.jpg" alt="AutoMIR — pestaña Flashcards" style="width: 90%; display: block; margin: 0 auto;" />

## Lo que aprendí

Pasé de estudiar todo el día a dedicarle, mucho mucho, 6 horas diarias eficientes. En esas seis horas estudio un tema nuevo, repaso los anteriores y respondo preguntas tipo MIR. Antes esas mismas seis horas se me iban solo en hacer resúmenes.

Pero más allá del programa, esto me dejó una conclusión que llevo dándole vueltas un tiempo: **no creo que el desarrollador vaya a desaparecer**.

El desarrollador no es solo alguien que escribe código. Tiene que saber **por qué** lo hace. Tiene que diseñar pensando en el cliente, en lo que se va a usar, en lo que tiene que verse bien. No es crear por crear y que funcione. Tiene que estar ajustado al usuario, ser bonito, ser eficiente.

Y esas cosas, por el momento, la IA no las reemplaza. La IA es un trabajador increíble cuando le das instrucciones claras. Pero alguien tiene que decidir qué construir, cómo organizarlo, qué tiene sentido y qué no. Ese alguien soy yo cuando me siento a pensar antes de abrir Claude.

Por eso quiero aprender a programar de verdad. No para reemplazar a Claude — para entender mejor lo que estoy construyendo con él.
