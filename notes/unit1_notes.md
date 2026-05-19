# Unit 1 - Notas Agentes IA

## ¿Qué es un agente?

Un agente de IA no es solamente un chatbot que responde texto. La diferencia es que el agente puede tomar decisiones y usar herramientas externas para resolver tareas. En este caso se usaron herramientas de búsqueda web para obtener información actualizada.

## Cosas importantes de la unidad

- El modelo funciona como el “cerebro” del agente.
- Las tools permiten que el agente interactúe con información externa.
- El flujo principal de un agente es:
  
Thought → Action → Observation → Final Answer

- Thought: el modelo piensa qué debe hacer.
- Action: ejecuta una herramienta o acción.
- Observation: analiza el resultado obtenido.
- Final Answer: genera la respuesta final.

## Experimentos realizados

### 1. Primer agente funcional

Se creó un agente usando:
- CodeAgent
- DuckDuckGoSearchTool
- InferenceClientModel

El agente pudo responder preguntas como:
- capital de Colombia
- presidente actual
- noticias recientes

## System prompts

También se probaron diferentes system prompts para cambiar el comportamiento del modelo.

Ejemplos:
- agente profesional de servicio al cliente
- agente rebelde que no sigue instrucciones

Esto mostró cómo el comportamiento del modelo cambia dependiendo del prompt del sistema.

## Tool Calling

Se realizó un ejemplo manual de tool calling usando una función de clima.

El modelo primero genera:
- Thought
- Action

Después se ejecuta la función manualmente y se devuelve:
- Observation

Finalmente el modelo genera:# Unit 1 - Notas Agentes IA

## ¿Qué es un agente?

Un agente de IA no es solamente un chatbot que responde texto. La diferencia es que el agente puede tomar decisiones y usar herramientas externas para resolver tareas. En este caso se usaron herramientas de búsqueda web para obtener información actualizada.

## Cosas importantes de la unidad

- El modelo funciona como el “cerebro” del agente.
- Las tools permiten que el agente interactúe con información externa.
- El flujo principal de un agente es:
  
Thought → Action → Observation → Final Answer

- Thought: el modelo piensa qué debe hacer.
- Action: ejecuta una herramienta o acción.
- Observation: analiza el resultado obtenido.
- Final Answer: genera la respuesta final.

## Experimentos realizados

### 1. Primer agente funcional

Se creó un agente usando:
- CodeAgent
- DuckDuckGoSearchTool
- InferenceClientModel

El agente pudo responder preguntas como:
- capital de Colombia
- presidente actual
- noticias recientes

## System prompts

También se probaron diferentes system prompts para cambiar el comportamiento del modelo.

Ejemplos:
- agente profesional de servicio al cliente
- agente rebelde que no sigue instrucciones

Esto mostró cómo el comportamiento del modelo cambia dependiendo del prompt del sistema.

## Tool Calling

Se realizó un ejemplo manual de tool calling usando una función de clima.

El modelo primero genera:
- Thought
- Action

Después se ejecuta la función manualmente y se devuelve:
- Observation

Finalmente el modelo genera:
- Final Answer

## Problemas encontrados

- Problemas iniciales con Python 3.6.
- Error al activar el entorno virtual en PowerShell.
- Dependencias faltantes como `ddgs`.
- Algunos imports del curso ya estaban desactualizados.

## Observaciones personales

Los agentes son más complejos que un chatbot normal porque combinan razonamiento, herramientas externas y ejecución de acciones. También se notó que muchas librerías cambian rápido y algunos ejemplos del curso dejan de funcionar exactamente igual.
- Final Answer

## Problemas encontrados

- Problemas iniciales con Python 3.6.
- Error al activar el entorno virtual en PowerShell.
- Dependencias faltantes como `ddgs`.
- Algunos imports del curso ya estaban desactualizados.

## Observaciones personales

Los agentes son más complejos que un chatbot normal porque combinan razonamiento, herramientas externas y ejecución de acciones. También se notó que muchas librerías cambian rápido y algunos ejemplos del curso dejan de funcionar exactamente igual.