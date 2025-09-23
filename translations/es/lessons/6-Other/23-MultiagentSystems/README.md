<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "38a1185ae3d54b180378bbd71ae3ef16",
  "translation_date": "2025-09-23T12:05:46+00:00",
  "source_file": "lessons/6-Other/23-MultiagentSystems/README.md",
  "language_code": "es"
}
-->
# Sistemas Multi-Agente

Una de las posibles formas de lograr inteligencia es el enfoque llamado **emergente** (o **sinérgico**), que se basa en el hecho de que el comportamiento combinado de muchos agentes relativamente simples puede resultar en un comportamiento general más complejo (o inteligente) del sistema en su conjunto. Teóricamente, esto se basa en los principios de [Inteligencia Colectiva](https://en.wikipedia.org/wiki/Collective_intelligence), [Emergentismo](https://en.wikipedia.org/wiki/Global_brain) y [Cibernética Evolutiva](https://en.wikipedia.org/wiki/Global_brain), que afirman que los sistemas de nivel superior obtienen algún tipo de valor añadido cuando se combinan adecuadamente a partir de sistemas de nivel inferior (el llamado *principio de transición de metasistema*).

## [Cuestionario previo a la clase](https://ff-quizzes.netlify.app/en/ai/quiz/45)

La dirección de los **Sistemas Multi-Agente** surgió en la IA en la década de 1990 como respuesta al crecimiento de Internet y los sistemas distribuidos. Uno de los libros de texto clásicos de IA, [Artificial Intelligence: A Modern Approach](https://en.wikipedia.org/wiki/Artificial_Intelligence:_A_Modern_Approach), se centra en la visión de la IA clásica desde el punto de vista de los sistemas multi-agente.

El concepto central del enfoque multi-agente es la noción de **Agente**: una entidad que vive en algún **entorno**, que puede percibir y sobre el cual puede actuar. Esta es una definición muy amplia, y puede haber muchos tipos y clasificaciones diferentes de agentes:

* Según su capacidad para razonar:
   - Los agentes **reactivos** suelen tener un comportamiento simple de tipo solicitud-respuesta.
   - Los agentes **deliberativos** emplean algún tipo de razonamiento lógico y/o capacidades de planificación.
* Según el lugar donde el agente ejecuta su código:
   - Los agentes **estáticos** trabajan en un nodo de red dedicado.
   - Los agentes **móviles** pueden mover su código entre nodos de red.
* Según su comportamiento:
   - Los agentes **pasivos** no tienen objetivos específicos. Estos agentes pueden reaccionar a estímulos externos, pero no iniciarán acciones por sí mismos.
   - Los agentes **activos** tienen algunos objetivos que persiguen.
   - Los agentes **cognitivos** implican planificación y razonamiento complejos.

Hoy en día, los sistemas multi-agente se utilizan en una serie de aplicaciones:

* En juegos, muchos personajes no jugadores emplean algún tipo de IA y pueden considerarse agentes inteligentes.
* En la producción de video, el renderizado de escenas 3D complejas que involucran multitudes se realiza típicamente mediante simulación multi-agente.
* En la modelización de sistemas, el enfoque multi-agente se utiliza para simular el comportamiento de un modelo complejo. Por ejemplo, el enfoque multi-agente se ha utilizado con éxito para predecir la propagación de la enfermedad COVID-19 a nivel mundial. Un enfoque similar puede usarse para modelar el tráfico en una ciudad y ver cómo reacciona a los cambios en las reglas de tráfico.
* En sistemas de automatización complejos, cada dispositivo puede actuar como un agente independiente, lo que hace que el sistema completo sea menos monolítico y más robusto.

No dedicaremos mucho tiempo a profundizar en los sistemas multi-agente, pero consideraremos un ejemplo de **Modelado Multi-Agente**.

## NetLogo

[NetLogo](https://ccl.northwestern.edu/netlogo/) es un entorno de modelado multi-agente basado en una versión modificada del lenguaje de programación [Logo](https://en.wikipedia.org/wiki/Logo_(programming_language)). Este lenguaje fue desarrollado para enseñar conceptos de programación a niños y permite controlar un agente llamado **tortuga**, que puede moverse dejando un rastro detrás. Esto permite crear figuras geométricas complejas, lo cual es una forma muy visual de entender el comportamiento de un agente.

En NetLogo, podemos crear muchas tortugas utilizando el comando `create-turtles`. Luego podemos ordenar a todas las tortugas que realicen algunas acciones (en el ejemplo a continuación: avanzar 10 puntos):

```
create-turtles 10
ask turtles [
  forward 10
]
```

Por supuesto, no es interesante cuando todas las tortugas hacen lo mismo, así que podemos `ask` a grupos de tortugas, por ejemplo, aquellas que están en las cercanías de un cierto punto. También podemos crear tortugas de diferentes *razas* utilizando el comando `breed [cats cat]`. Aquí `cat` es el nombre de una raza, y necesitamos especificar tanto la palabra en singular como en plural, porque diferentes comandos usan diferentes formas para mayor claridad.

> ✅ No profundizaremos en el aprendizaje del lenguaje NetLogo en sí: puedes visitar el excelente recurso [Beginner's Interactive NetLogo Dictionary](https://ccl.northwestern.edu/netlogo/bind/) si estás interesado en aprender más.

Puedes [descargar](https://ccl.northwestern.edu/netlogo/download.shtml) e instalar NetLogo para probarlo.

### Biblioteca de Modelos

Una gran ventaja de NetLogo es que contiene una biblioteca de modelos funcionales que puedes probar. Ve a **File &rightarrow; Models Library**, y tendrás muchas categorías de modelos para elegir.

<img alt="Biblioteca de Modelos de NetLogo" src="images/NetLogo-ModelLib.png" width="60%"/>

> Una captura de pantalla de la biblioteca de modelos por Dmitry Soshnikov

Puedes abrir uno de los modelos, por ejemplo **Biology &rightarrow; Flocking**.

### Principios Básicos

Después de abrir el modelo, serás llevado a la pantalla principal de NetLogo. Aquí hay un modelo de ejemplo que describe la población de lobos y ovejas, dadas recursos finitos (hierba).

![Pantalla Principal de NetLogo](../../../../../translated_images/NetLogo-Main.32653711ec1a01b3cab22ec0b148e64193d0b979b055285bef329d5e3d6958c5.es.png)

> Captura de pantalla por Dmitry Soshnikov

En esta pantalla, puedes ver:

* La sección **Interface**, que contiene:
  - El campo principal, donde viven todos los agentes.
  - Diferentes controles: botones, deslizadores, etc.
  - Gráficos que puedes usar para mostrar parámetros de la simulación.
* La pestaña **Code**, que contiene el editor donde puedes escribir el programa NetLogo.

En la mayoría de los casos, la interfaz tendrá un botón **Setup**, que inicializa el estado de la simulación, y un botón **Go**, que inicia la ejecución. Estos son manejados por los controladores correspondientes en el código que se ven así:

```
to go [
...
]
```

El mundo de NetLogo consiste en los siguientes objetos:

* **Agentes** (tortugas) que pueden moverse por el campo y hacer algo. Ordenas a los agentes utilizando la sintaxis `ask turtles [...]`, y el código entre corchetes es ejecutado por todos los agentes en *modo tortuga*.
* **Parches** son áreas cuadradas del campo, en las que viven los agentes. Puedes referirte a todos los agentes en el mismo parche, o puedes cambiar los colores del parche y algunas otras propiedades. También puedes `ask patches` que hagan algo.
* **Observador** es un agente único que controla el mundo. Todos los controladores de botones se ejecutan en *modo observador*.

> ✅ La belleza de un entorno multi-agente es que el código que se ejecuta en modo tortuga o en modo parche es ejecutado al mismo tiempo por todos los agentes en paralelo. Así, al escribir un poco de código y programar el comportamiento de un agente individual, puedes crear un comportamiento complejo del sistema de simulación en su conjunto.

### Flocking

Como ejemplo de comportamiento multi-agente, consideremos el **[Flocking](https://en.wikipedia.org/wiki/Flocking_(behavior))**. Flocking es un patrón complejo que es muy similar a cómo vuelan las bandadas de aves. Al observarlas volar, podrías pensar que siguen algún tipo de algoritmo colectivo, o que poseen alguna forma de *inteligencia colectiva*. Sin embargo, este comportamiento complejo surge cuando cada agente individual (en este caso, un *pájaro*) solo observa a algunos otros agentes a corta distancia de él y sigue tres reglas simples:

* **Alineación**: se dirige hacia la dirección promedio de los agentes vecinos.
* **Cohesión**: intenta dirigirse hacia la posición promedio de los vecinos (*atracción a largo alcance*).
* **Separación**: cuando se acerca demasiado a otros pájaros, intenta alejarse (*repulsión a corto alcance*).

Puedes ejecutar el ejemplo de flocking y observar el comportamiento. También puedes ajustar parámetros, como el *grado de separación* o el *rango de visión*, que define qué tan lejos puede ver cada pájaro. Ten en cuenta que si reduces el rango de visión a 0, todos los pájaros se vuelven ciegos y el flocking se detiene. Si reduces la separación a 0, todos los pájaros se agrupan en una línea recta.

> ✅ Cambia a la pestaña **Code** y observa dónde se implementan en el código las tres reglas de flocking (alineación, cohesión y separación). Nota cómo solo nos referimos a aquellos agentes que están a la vista.

### Otros Modelos para Ver

Hay algunos modelos más interesantes que puedes experimentar:

* **Art &rightarrow; Fireworks** muestra cómo un fuego artificial puede considerarse un comportamiento colectivo de corrientes individuales de fuego.
* **Social Science &rightarrow; Traffic Basic** y **Social Science &rightarrow; Traffic Grid** muestran el modelo de tráfico urbano en una cuadrícula 1D y 2D con o sin semáforos. Cada coche en la simulación sigue las siguientes reglas:
   - Si el espacio frente a él está vacío, acelera (hasta una cierta velocidad máxima).
   - Si ve un obstáculo frente a él, frena (y puedes ajustar qué tan lejos puede ver un conductor).
* **Social Science &rightarrow; Party** muestra cómo las personas se agrupan durante una fiesta de cóctel. Puedes encontrar la combinación de parámetros que conduce al aumento más rápido de la felicidad del grupo.

Como puedes ver en estos ejemplos, las simulaciones multi-agente pueden ser una forma bastante útil de entender el comportamiento de un sistema complejo compuesto por individuos que siguen la misma lógica o una lógica similar. También puede usarse para controlar agentes virtuales, como [NPCs](https://en.wikipedia.org/wiki/NPC) en videojuegos, o agentes en mundos animados en 3D.

## Agentes Deliberativos

Los agentes descritos anteriormente son muy simples, reaccionando a los cambios en el entorno utilizando algún tipo de algoritmo. Como tal, son **agentes reactivos**. Sin embargo, a veces los agentes pueden razonar y planificar sus acciones, en cuyo caso se les llama **deliberativos**.

Un ejemplo típico sería un agente personal que recibe una instrucción de un humano para reservar un paquete de vacaciones. Supongamos que hay muchos agentes que viven en internet y que pueden ayudarle. Entonces debería contactar a otros agentes para ver qué vuelos están disponibles, cuáles son los precios de los hoteles para diferentes fechas y tratar de negociar el mejor precio. Cuando el plan de vacaciones esté completo y confirmado por el propietario, puede proceder con la reserva.

Para hacer esto, los agentes necesitan **comunicarse**. Para una comunicación exitosa necesitan:

* Algunos **lenguajes estándar para intercambiar conocimiento**, como [Knowledge Interchange Format](https://en.wikipedia.org/wiki/Knowledge_Interchange_Format) (KIF) y [Knowledge Query and Manipulation Language](https://en.wikipedia.org/wiki/Knowledge_Query_and_Manipulation_Language) (KQML). Estos lenguajes están diseñados basándose en la [teoría de los actos de habla](https://en.wikipedia.org/wiki/Speech_act).
* Estos lenguajes también deben incluir algunos **protocolos para negociaciones**, basados en diferentes **tipos de subastas**.
* Una **ontología común** para usar, de modo que se refieran a los mismos conceptos conociendo su semántica.
* Una forma de **descubrir** lo que diferentes agentes pueden hacer, también basada en algún tipo de ontología.

Los agentes deliberativos son mucho más complejos que los reactivos, porque no solo reaccionan a los cambios en el entorno, sino que también deben ser capaces de *iniciar* acciones. Una de las arquitecturas propuestas para agentes deliberativos es el llamado agente de Creencias-Deseos-Intenciones (BDI):

* **Creencias** forman un conjunto de conocimiento sobre el entorno del agente. Puede estructurarse como una base de conocimiento o un conjunto de reglas que un agente puede aplicar a una situación específica en el entorno.
* **Deseos** definen lo que un agente quiere hacer, es decir, sus objetivos. Por ejemplo, el objetivo del agente asistente personal mencionado anteriormente es reservar un paquete de vacaciones, y el objetivo de un agente de hotel es maximizar las ganancias.
* **Intenciones** son acciones específicas que un agente planea para alcanzar sus objetivos. Las acciones típicamente cambian el entorno y causan comunicación con otros agentes.

Existen algunas plataformas disponibles para construir sistemas multi-agente, como [JADE](https://jade.tilab.com/). [Este artículo](https://arxiv.org/ftp/arxiv/papers/2007/2007.08961.pdf) contiene una revisión de plataformas multi-agente, junto con una breve historia de los sistemas multi-agente y sus diferentes escenarios de uso.

## Conclusión

Los sistemas multi-agente pueden tomar formas muy diferentes y usarse en muchas aplicaciones distintas. 
Todos tienden a centrarse en el comportamiento más simple de un agente individual y logran un comportamiento más complejo del sistema general debido al **efecto sinérgico**.

## 🚀 Desafío

Lleva esta lección al mundo real e intenta conceptualizar un sistema multi-agente que pueda resolver un problema. ¿Qué, por ejemplo, necesitaría hacer un sistema multi-agente para optimizar una ruta de autobús escolar? ¿Cómo podría funcionar en una panadería?

## [Cuestionario posterior a la clase](https://ff-quizzes.netlify.app/en/ai/quiz/46)

## Revisión y Autoestudio

Revisa el uso de este tipo de sistema en la industria. Elige un dominio como la manufactura o la industria de los videojuegos y descubre cómo los sistemas multi-agente pueden usarse para resolver problemas únicos.

## [Tarea de NetLogo](assignment.md)

---

