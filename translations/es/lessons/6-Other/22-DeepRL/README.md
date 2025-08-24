<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "dbacf9b1915612981d76059678e563e5",
  "translation_date": "2025-08-24T09:20:54+00:00",
  "source_file": "lessons/6-Other/22-DeepRL/README.md",
  "language_code": "es"
}
-->
# Aprendizaje por Refuerzo Profundo

El aprendizaje por refuerzo (RL, por sus siglas en inglés) se considera uno de los paradigmas básicos del aprendizaje automático, junto con el aprendizaje supervisado y no supervisado. Mientras que en el aprendizaje supervisado dependemos de un conjunto de datos con resultados conocidos, el RL se basa en **aprender haciendo**. Por ejemplo, cuando vemos un videojuego por primera vez, comenzamos a jugar, incluso sin conocer las reglas, y pronto somos capaces de mejorar nuestras habilidades simplemente jugando y ajustando nuestro comportamiento.

## [Cuestionario previo a la lección](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/122)

Para realizar RL, necesitamos:

* Un **entorno** o **simulador** que establezca las reglas del juego. Deberíamos poder ejecutar experimentos en el simulador y observar los resultados.
* Alguna **función de recompensa**, que indique qué tan exitoso fue nuestro experimento. En el caso de aprender a jugar un videojuego, la recompensa sería nuestra puntuación final.

Basándonos en la función de recompensa, deberíamos ser capaces de ajustar nuestro comportamiento y mejorar nuestras habilidades, de modo que la próxima vez juguemos mejor. La principal diferencia entre otros tipos de aprendizaje automático y RL es que en RL típicamente no sabemos si ganamos o perdemos hasta que terminamos el juego. Por lo tanto, no podemos decir si un movimiento en particular es bueno o no; solo recibimos una recompensa al final del juego.

Durante el RL, típicamente realizamos muchos experimentos. En cada experimento, necesitamos equilibrar entre seguir la estrategia óptima que hemos aprendido hasta ahora (**explotación**) y explorar nuevos estados posibles (**exploración**).

## OpenAI Gym

Una gran herramienta para RL es el [OpenAI Gym](https://gym.openai.com/): un **entorno de simulación** que puede simular muchos entornos diferentes, desde juegos de Atari hasta la física detrás del equilibrio de un poste. Es uno de los entornos de simulación más populares para entrenar algoritmos de aprendizaje por refuerzo y es mantenido por [OpenAI](https://openai.com/).

> **Nota**: Puedes ver todos los entornos disponibles en OpenAI Gym [aquí](https://gym.openai.com/envs/#classic_control).

## Equilibrio de CartPole

Probablemente todos han visto dispositivos modernos de equilibrio como el *Segway* o los *Gyroscooters*. Son capaces de equilibrarse automáticamente ajustando sus ruedas en respuesta a una señal de un acelerómetro o giroscopio. En esta sección, aprenderemos a resolver un problema similar: equilibrar un poste. Es similar a la situación en la que un artista de circo necesita equilibrar un poste en su mano, pero este equilibrio ocurre solo en 1D.

Una versión simplificada de este problema se conoce como el problema de **CartPole**. En el mundo de CartPole, tenemos un deslizador horizontal que puede moverse hacia la izquierda o la derecha, y el objetivo es equilibrar un poste vertical sobre el deslizador mientras se mueve.

<img alt="un cartpole" src="images/cartpole.png" width="200"/>

Para crear y usar este entorno, necesitamos unas pocas líneas de código en Python:

```python
import gym
env = gym.make("CartPole-v1")

env.reset()
done = False
total_reward = 0
while not done:
   env.render()
   action = env.action_space.sample()
   observaton, reward, done, info = env.step(action)
   total_reward += reward

print(f"Total reward: {total_reward}")
```

Cada entorno puede ser accedido exactamente de la misma manera:
* `env.reset` inicia un nuevo experimento.
* `env.step` realiza un paso de simulación. Recibe una **acción** del **espacio de acciones** y devuelve una **observación** (del espacio de observación), así como una recompensa y una bandera de terminación.

En el ejemplo anterior, realizamos una acción aleatoria en cada paso, por lo que la duración del experimento es muy corta:

![cartpole sin equilibrio](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-nobalance.gif)

El objetivo de un algoritmo de RL es entrenar un modelo, la llamada **política** π, que devolverá la acción en respuesta a un estado dado. También podemos considerar la política como probabilística, es decir, para cualquier estado *s* y acción *a*, devolverá la probabilidad π(*a*|*s*) de que deberíamos tomar *a* en el estado *s*.

## Algoritmo de Gradientes de Política

La forma más obvia de modelar una política es creando una red neuronal que tome estados como entrada y devuelva las acciones correspondientes (o más bien las probabilidades de todas las acciones). En cierto sentido, sería similar a una tarea de clasificación normal, con una gran diferencia: no sabemos de antemano qué acciones deberíamos tomar en cada paso.

La idea aquí es estimar esas probabilidades. Construimos un vector de **recompensas acumulativas** que muestra nuestra recompensa total en cada paso del experimento. También aplicamos un **descuento de recompensas** multiplicando las recompensas anteriores por un coeficiente γ=0.99, para disminuir la importancia de las recompensas más antiguas. Luego, reforzamos aquellos pasos a lo largo del camino del experimento que producen mayores recompensas.

> Aprende más sobre el algoritmo de Gradientes de Política y míralo en acción en el [notebook de ejemplo](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb).

## Algoritmo Actor-Critic

Una versión mejorada del enfoque de Gradientes de Política se llama **Actor-Critic**. La idea principal detrás de este enfoque es que la red neuronal se entrene para devolver dos cosas:

* La política, que determina qué acción tomar. Esta parte se llama **actor**.
* La estimación de la recompensa total que podemos esperar obtener en este estado; esta parte se llama **critic**.

En cierto sentido, esta arquitectura se asemeja a un [GAN](../../4-ComputerVision/10-GANs/README.md), donde tenemos dos redes que se entrenan una contra la otra. En el modelo actor-critic, el actor propone la acción que necesitamos tomar, y el crítico intenta ser crítico y estimar el resultado. Sin embargo, nuestro objetivo es entrenar estas redes en conjunto.

Dado que conocemos tanto las recompensas acumulativas reales como los resultados devueltos por el crítico durante el experimento, es relativamente fácil construir una función de pérdida que minimice la diferencia entre ellos. Eso nos daría la **pérdida del crítico**. Podemos calcular la **pérdida del actor** utilizando el mismo enfoque que en el algoritmo de gradientes de política.

Después de ejecutar uno de estos algoritmos, podemos esperar que nuestro CartPole se comporte así:

![cartpole equilibrado](../../../../../lessons/6-Other/22-DeepRL/images/cartpole-balance.gif)

## ✍️ Ejercicios: Gradientes de Política y Actor-Critic RL

Continúa tu aprendizaje en los siguientes notebooks:

* [RL en TensorFlow](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-TF.ipynb)
* [RL en PyTorch](../../../../../lessons/6-Other/22-DeepRL/CartPole-RL-PyTorch.ipynb)

## Otras Tareas de RL

El aprendizaje por refuerzo es actualmente un campo de investigación en rápido crecimiento. Algunos ejemplos interesantes de aprendizaje por refuerzo son:

* Enseñar a una computadora a jugar **juegos de Atari**. La parte desafiante de este problema es que no tenemos un estado simple representado como un vector, sino más bien una captura de pantalla, y necesitamos usar una CNN para convertir esta imagen en un vector de características o para extraer información de recompensa. Los juegos de Atari están disponibles en el Gym.
* Enseñar a una computadora a jugar juegos de mesa, como Ajedrez y Go. Recientemente, programas de última generación como **Alpha Zero** fueron entrenados desde cero por dos agentes jugando entre sí y mejorando en cada paso.
* En la industria, el RL se utiliza para crear sistemas de control a partir de simulaciones. Un servicio llamado [Bonsai](https://azure.microsoft.com/services/project-bonsai/?WT.mc_id=academic-77998-cacaste) está diseñado específicamente para eso.

## Conclusión

Ahora hemos aprendido cómo entrenar agentes para lograr buenos resultados simplemente proporcionándoles una función de recompensa que define el estado deseado del juego y dándoles la oportunidad de explorar inteligentemente el espacio de búsqueda. Hemos probado con éxito dos algoritmos y logrado un buen resultado en un período de tiempo relativamente corto. Sin embargo, este es solo el comienzo de tu viaje en RL, y definitivamente deberías considerar tomar un curso separado si deseas profundizar más.

## 🚀 Desafío

Explora las aplicaciones enumeradas en la sección 'Otras Tareas de RL' e intenta implementar una.

## [Cuestionario posterior a la lección](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/222)

## Revisión y Autoestudio

Aprende más sobre el aprendizaje por refuerzo clásico en nuestro [Currículo de Aprendizaje Automático para Principiantes](https://github.com/microsoft/ML-For-Beginners/blob/main/8-Reinforcement/README.md).

Mira [este excelente video](https://www.youtube.com/watch?v=qv6UVOQ0F44) que habla sobre cómo una computadora puede aprender a jugar Super Mario.

## Asignación: [Entrena un Mountain Car](lab/README.md)

Tu objetivo durante esta asignación será entrenar un entorno diferente de Gym: [Mountain Car](https://www.gymlibrary.ml/environments/classic_control/mountain_car/).

**Descargo de responsabilidad**:  
Este documento ha sido traducido utilizando el servicio de traducción automática [Co-op Translator](https://github.com/Azure/co-op-translator). Aunque nos esforzamos por garantizar la precisión, tenga en cuenta que las traducciones automatizadas pueden contener errores o imprecisiones. El documento original en su idioma nativo debe considerarse la fuente autorizada. Para información crítica, se recomienda una traducción profesional realizada por humanos. No nos hacemos responsables de malentendidos o interpretaciones erróneas que puedan surgir del uso de esta traducción.