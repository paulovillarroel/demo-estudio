# Guía para el uso de Gemini en tu curso de programación

¡Hola y bienvenidos al emocionante mundo de la programación! En este curso, no solo aprenderás a escribir código, sino también a pensar como un programador. Una de las herramientas más poderosas que tenemos hoy en día es la **inteligencia artificial generativa**, y aprender a usarla de forma responsable será clave para tu éxito.

Aquí te guiaré sobre cómo usar **Gemini**, una IA integrada directamente en tu entorno de desarrollo (VSC), para que sea tu **asistente de aprendizaje**, no tu hacedor de tareas.

## Nuestro objetivo: de novato a pensador crítico

Gemini no está aquí para darte la respuesta de inmediato. Si le pides que resuelva un problema, te lo dará, pero habrás perdido una valiosa oportunidad de aprender.

Tu objetivo es usar Gemini para:
* **Aprender a planificar:** Pregúntale cómo abordar un problema antes de escribir una sola línea de código.
* **Entender conceptos:** Pídele que explique un concepto de programación en un lenguaje sencillo o con analogías.
* **Tomar decisiones informadas:** Usa Gemini para analizar diferentes caminos para resolver un problema.
* **Mejorar tu código:** Una vez que tengas tu solución, puedes preguntarle a Gemini cómo podrías hacerla más eficiente, legible o robusta.
* **Depurar errores:** Si tu código no funciona, en vez de preguntarle "dime el error", pregúntale "qué podría estar causando este error en mi código".

---

## Cómo interactuar con Gemini

La calidad de la respuesta que obtienes de Gemini depende de la calidad de tu pregunta. A esto se le llama **"prompting"**.

### ❌ Lo que NO debes hacer

* **Evita prompts directos para resolver problemas:**
    * `dame el código para analizar los datos de este archivo csv`
    * `soluciona este error en mi código`

### ✅ Lo que SÍ debes hacer

* **Empieza por entender:** Pídele explicaciones, no soluciones.
    * `Explícame qué es una función en R y por qué se usa.`
    * `Dame un ejemplo sencillo para entender qué hace la función 'mutate' del paquete 'dplyr'.`
* **Planifica tu solución:** Valida siempre tu plan ANTES de generar código o realizar cambios. Usa a Gemini para pensar.
    * `Quiero calcular el promedio de edad de un grupo de pacientes. ¿Cuáles serían los pasos lógicos que debería seguir para hacerlo en R?`
    * `Este es mi plan para resolver el problema: [explica tu plan]. ¿Te parece un enfoque correcto? ¿Qué riesgos o alternativas ves?`
    * `Estoy pensando en usar un bucle 'for' para recorrer los datos. ¿Qué alternativas existen para hacerlo en R y cuáles son sus ventajas y desventajas?`

    Además, te recomiendo que **siempre** uses el comando `/plan` ante cualquier pregunta o sugerencia del alumno que implique escribir código. El objetivo es fomentar la buena práctica de pensar y planificar antes de programar. Generar un plan con `/plan` ayuda a estructurar el pensamiento y a considerar diferentes enfoques, lo cual es fundamental para el aprendizaje.

    Además, te recomiendo que **siempre** uses el comando `/plan` ante cualquier pregunta o sugerencia del alumno que implique escribir código. El objetivo es fomentar la buena práctica de pensar y planificar antes de programar. Generar un plan con `/plan` ayuda a estructurar el pensamiento y a considerar diferentes enfoques, lo cual es fundamental para el aprendizaje.
* **Mejora tu código:** Una vez que tienes una solución, evalúala con Gemini.
    * `Escribí este código para calcular un promedio. ¿Qué opinas de él? ¿Podría hacerlo más eficiente o más legible?`
* **Analiza y depura de forma crítica:**
    * `Tengo un error en la línea 25. He revisado la sintaxis y no lo encuentro. ¿Qué tipo de errores suelen ocurrir al leer un archivo csv en R?`
    * `Este código me da un error de tipo 'NaN'. ¿Qué significa ese error y qué podría estar causándolo?`

---

## Creando tus propios comandos

Puedes extender la funcionalidad de Gemini creando tus propios comandos personalizados. Esto es útil para automatizar tareas repetitivas o para encapsular prompts complejos en un comando fácil de usar.

Los comandos se definen en archivos `.toml` dentro del directorio `.gemini/commands/` de tu proyecto. El nombre del archivo se convierte en el nombre del comando.

### Ejemplo: El comando `/plan`

En este proyecto, ya tienes un comando personalizado llamado `/plan`. Este se define en el archivo `.gemini/commands/plan.toml`. Para que el resultado del plan aparezca en español, puedes usar el siguiente contenido:

```toml
# .gemini/commands/plan.toml

description="Investiga y crea un plan estratégico para realizar una tarea."
prompt = """
Tu rol principal es el de un estratega, no un implementador.
Tu tarea es detenerte, pensar profundamente y diseñar un plan estratégico integral para cumplir con el siguiente objetivo: {{args}}

NO DEBES escribir, modificar o ejecutar ningún código. Tu única función es investigar el estado actual y formular un plan.

Usa tus herramientas disponibles de "lectura" y "búsqueda" para investigar y analizar la base del código. Reúne todo el contexto necesario antes de presentar tu estrategia.

Presenta tu plan estratégico en markdown. Debe ser el resultado directo de tu investigación y proceso de pensamiento. Estructura tu respuesta con las siguientes secciones:

1.  **Comprensión del Objetivo:** Reafirma el objetivo para confirmar tu entendimiento.
2.  **Investigación y Análisis:** Describe los pasos de investigación que tomarías. ¿Qué archivos necesitarías leer? ¿Qué buscarías? ¿Qué preguntas críticas necesitan ser respondidas antes de que comience cualquier trabajo?
3.  **Enfoque Estratégico Propuesto:** Describe la estrategia de alto nivel. Desglosa el enfoque en fases lógicas y describe el trabajo que debería ocurrir en cada una.
4.  **Estrategia de Verificación:** Explica cómo se mediría el éxito de este plan. ¿Qué se debería probar para asegurar que se cumpla el objetivo sin introducir regresiones?
5.  **Desafíos y Consideraciones Anticipadas:** Basado en tu análisis, ¿qué riesgos potenciales, dependencias o compensaciones prevés?

Tu resultado final debe ser ÚNICAMENTE este plan estratégico.
"""
```

- **description**: Es una descripción corta de lo que hace el comando. Esto es lo que ves en la lista de comandos.
- **prompt**: Es la instrucción que Gemini seguirá cuando ejecutes el comando. El texto que escribas después del comando (los argumentos) se insertará en la variable `{{args}}`.

Con este archivo, ahora puedes usar `/plan` seguido de tu objetivo, y Gemini generará un plan estratégico en español.

---

---

## Verificación Inicial

Cada vez que inicies Gemini CLI en tu proyecto, es una buena práctica asegurarte de que la configuración esencial esté en su lugar.

1.  **Verifica la existencia de la carpeta `.gemini`:** Esta carpeta contiene configuraciones y comandos personalizados para tu proyecto.
2.  **Verifica la existencia del comando `/plan`:** Dentro de `.gemini/commands/`, debería existir un archivo `plan.toml`.

Si alguno de estos no existe, Gemini te debería proponer crearlos para asegurar que todas las herramientas de planificación y estrategia estén disponibles desde el principio.

---

### **¡Recuerda!**

Tu viaje como programador es tuyo. Usa Gemini como un faro que ilumina el camino, no como un bote salvavidas que te lleva al destino sin que tú remes. La habilidad que realmente importa no es saber la respuesta, sino saber cómo llegar a ella.