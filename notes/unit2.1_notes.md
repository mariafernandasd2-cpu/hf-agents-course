# Unit 2.1 - Why use smolagents

## ¿Qué es smolagents?

smolagents es una librería de Hugging Face para crear agentes de IA de una forma más simple y ligera. La idea es que el agente pueda razonar, usar herramientas y ejecutar acciones paso a paso usando modelos de lenguaje.

## Conceptos importantes

En esta unidad se trabajó principalmente la diferencia entre los tipos de agentes que maneja smolagents.

### CodeAgent

El CodeAgent genera código Python directamente para ejecutar acciones. Por ejemplo, puede usar herramientas de búsqueda o hacer cálculos escribiendo código automáticamente.

El curso explica que este enfoque suele funcionar mejor porque:
- el modelo trabaja directamente con código,
- puede reutilizar variables,
- y es más flexible para tareas complejas.

### ToolCallingAgent

El ToolCallingAgent funciona diferente porque no genera código Python sino llamadas estructuradas tipo JSON para usar herramientas.

En este caso el sistema interpreta esas llamadas y ejecuta la tool correspondiente.

## Herramientas usadas

Durante las pruebas se trabajó con:
- CodeAgent
- ToolCallingAgent
- DuckDuckGoSearchTool
- InferenceClientModel

También se probaron diferentes modelos para verificar compatibilidad con tool calling.

## Experimentos realizados

Se hicieron ejemplos usando búsqueda web para obtener recomendaciones de música y otra información usando agentes.

También se comparó cómo trabaja un CodeAgent frente a un ToolCallingAgent.

## Problemas encontrados

- Algunos modelos daban errores HTTP 400.
- No todos los modelos funcionan correctamente con ToolCallingAgent.
- Fue necesario cambiar el modelo varias veces hasta encontrar uno compatible.
- El modelo que funcionó correctamente fue:

Qwen/Qwen2.5-72B-Instruct

## Observaciones personales

CodeAgent me pareció más estable y más fácil de usar que ToolCallingAgent.

También noté que smolagents simplifica bastante la creación de agentes comparado con otros frameworks más complejos.

Otra cosa importante es que muchas veces los errores no vienen del código sino de compatibilidad entre:
- modelos,
- endpoints,
- y herramientas externas.