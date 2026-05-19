# Unit 4 - Final Project (GAIA Agent)

## Introducción

En esta unidad final desarrollé un agente inspirado en el benchmark GAIA utilizando LangGraph, LangChain y herramientas externas.

El objetivo era construir un agente capaz de:
- responder preguntas,
- utilizar herramientas,
- buscar información,
- ejecutar cálculos,
- y resolver tareas similares a las del benchmark GAIA.

---

# ¿Qué es GAIA?

GAIA es un benchmark diseñado para evaluar agentes de inteligencia artificial en tareas del mundo real.

Las preguntas requieren:
- razonamiento,
- retrieval,
- navegación,
- uso de herramientas,
- planificación multi-step.

GAIA busca medir qué tan cerca están los agentes actuales de comportarse como asistentes generales reales.

---

# Objetivo del proyecto

El objetivo del proyecto fue crear un agente funcional capaz de resolver preguntas simples similares a las de nivel 1 de GAIA.

El agente debía:
- recibir preguntas,
- decidir qué herramienta usar,
- ejecutar acciones,
- y devolver respuestas.

---

# Arquitectura utilizada

El proyecto fue construido usando:
- LangGraph
- LangChain
- tools
- StateGraph
- routing lógico

La arquitectura principal fue:

```python
StateGraph
```

con:
- nodos,
- estados,
- herramientas,
- y flujo controlado.

---

# Modelo utilizado

Inicialmente el curso utiliza:
- GPT-4o,
- OpenAI APIs,
- tool-calling avanzado.

Sin embargo, mi entorno presentó varios problemas de compatibilidad relacionados con:
- APIs pagas,
- async workflows,
- modelos incompatibles,
- chat templates,
- y versiones de librerías.

Por esta razón utilicé:

```python
gpt2
```

usando:

```python
pipeline(
    "text-generation",
    model="gpt2"
)
```

Esto permitió ejecutar el proyecto localmente de manera estable.

---

# Herramientas implementadas

## Web Search Tool

Utilicé:

```python
DuckDuckGoSearchRun
```

para búsquedas web.

Ejemplo:

```python
search_tool.invoke(question)
```

---

## Calculator Tool

Construí una herramienta matemática usando:

```python
eval()
```

La herramienta podía resolver expresiones simples.

Ejemplo:

```python
25 * 12
```

---

## Weather Tool

También implementé una herramienta simple de clima.

Ejemplo:

```python
The weather in Paris is clear.
```

---

# Estado del agente

El estado principal fue:

```python
class AgentState(TypedDict):
    question: str
    answer: str
```

El agente almacenaba:
- la pregunta,
- y la respuesta generada.

---

# Flujo del agente

El flujo general fue:

1. recibir pregunta,
2. analizar contenido,
3. decidir herramienta,
4. ejecutar herramienta,
5. devolver respuesta.

La lógica principal se implementó usando:

```python
if "weather" in question
```

y verificaciones similares.

---

# Uso de LangGraph

El agente fue construido usando:

```python
StateGraph
```

con:
- START,
- END,
- nodos,
- y edges.

Ejemplo:

```python
builder.add_edge(START, "agent")
```

Finalmente el flujo se ejecutó usando:

```python
graph.invoke()
```

---

# Problemas encontrados

## Problemas con OpenAI

Muchos ejemplos oficiales dependían de:
- GPT-4o,
- OpenAI API,
- modelos pagos.

Esto generó errores de autenticación y compatibilidad.

---

## Problemas con Hugging Face

También aparecieron errores relacionados con:
- text2text-generation,
- chat_template,
- ChatHuggingFace,
- modelos incompatibles.

La solución fue simplificar el proyecto usando GPT2 y herramientas locales más estables.

---

## Problemas con async

Algunos notebooks generaban errores como:
- event loop closed,
- await issues,
- async incompatibilities.

Por eso se evitó utilizar workflows async complejos.

---

# Lo que aprendí

- Cómo construir agentes con LangGraph.
- Cómo usar herramientas externas.
- Cómo implementar routing lógico.
- Cómo integrar retrieval y búsqueda.
- Cómo adaptar proyectos cuando existen incompatibilidades de entorno.
- Cómo funcionan benchmarks como GAIA.

---

# Conclusión

Esta unidad permitió integrar todos los conceptos vistos durante el curso:
- agentes,
- tools,
- retrieval,
- LangGraph,
- workflows,
- razonamiento,
- y orchestration.

Aunque el proyecto fue simplificado respecto al template oficial, logró mantener:
- la arquitectura principal,
- los conceptos clave,
- y el comportamiento general esperado de un agente tipo GAIA.

Finalmente construí un agente funcional capaz de resolver tareas simples utilizando múltiples herramientas y control de flujo mediante LangGraph.