# Unit 3 - Agentic RAG

## Introducción

En esta unidad trabajé con Agentic RAG (Retrieval Augmented Generation) usando herramientas, retrieval y agentes para ayudar a Alfred a organizar una gala.

La idea principal fue construir un sistema capaz de:
- recuperar información sobre invitados,
- usar herramientas externas,
- consultar información actualizada,
- y responder preguntas utilizando distintas fuentes de información.

El objetivo era crear un agente más útil y contextualizado en vez de depender únicamente del conocimiento interno de un modelo de lenguaje.

---

# ¿Qué es RAG?

RAG significa Retrieval Augmented Generation.

La idea es:
1. buscar información relevante,
2. recuperar documentos,
3. enviar esa información al modelo,
4. generar una respuesta basada en contexto actualizado.

Esto ayuda a resolver el problema de que los LLMs:
- no siempre tienen información reciente,
- pueden alucinar,
- o no conocen datos específicos de un proyecto.

---

# ¿Qué es Agentic RAG?

Agentic RAG lleva RAG un paso más allá.

En vez de simplemente recuperar documentos automáticamente, el agente puede:
- decidir qué herramienta usar,
- combinar varias herramientas,
- buscar información externa,
- recuperar documentos,
- y luego construir una respuesta final.

El agente actúa de manera más dinámica y organizada.

---

# Retriever de invitados

Primero trabajé con un dataset de invitados usando:

```python
datasets.load_dataset()
```

El dataset contenía:
- nombres,
- relaciones,
- descripciones,
- emails.

Después convertí cada invitado en un objeto `Document`.

Ejemplo:

```python
Document(
    page_content="...",
    metadata={"name": guest["name"]}
)
```

---

# BM25Retriever

Para hacer retrieval utilicé:

```python
BM25Retriever
```

Este retriever permite buscar documentos relevantes utilizando coincidencias de texto.

Ejemplo:

```python
results = bm25_retriever.invoke("Ada Lovelace")
```

Luego imprimí:

```python
print(results[0].page_content)
```

---

# Tool de retrieval

Después convertí el retriever en una tool usando:

```python
Tool
```

La función principal fue:

```python
def extract_text(query: str) -> str:
```

Esta función:
- recibe una consulta,
- ejecuta retrieval,
- devuelve los documentos encontrados.

Finalmente se creó:

```python
guest_info_tool = Tool(
    name="guest_info_retriever",
    func=extract_text,
    description="Retrieves information about gala guests."
)
```

---

# DuckDuckGo Search Tool

También integré búsqueda web usando:

```python
DuckDuckGoSearchRun
```

Ejemplo:

```python
search_tool.invoke(
    "Who is the current president of France?"
)
```

Esto permitió consultar información externa en tiempo real.

---

# Weather Tool

Construí una tool personalizada para simular clima.

La función generaba:
- condición climática,
- temperatura.

Ejemplo:

```python
Weather in Paris: Clear, 25°C
```

La tool fue creada usando:

```python
weather_info_tool = Tool(
    name="get_weather_info",
    func=get_weather_info,
    description="Gets weather information."
)
```

---

# Hugging Face Hub Stats Tool

También creé una herramienta para consultar modelos populares del Hugging Face Hub.

Usé:

```python
from huggingface_hub import list_models
```

La función buscaba:
- el modelo más descargado,
- según un autor específico.

Ejemplo:

```python
hub_stats_tool.invoke("facebook")
```

Resultado:

```python
The most downloaded model by facebook is facebook/opt-125m with 9,414,291 downloads.
```

---

# Problemas encontrados

## Error con `direction`

Inicialmente apareció:

```python
TypeError: list_models() got an unexpected keyword argument 'direction'
```

Esto ocurrió porque la versión instalada de `huggingface_hub` era diferente a la usada en el curso.

La solución fue eliminar:

```python
direction=-1
```

y dejar únicamente:

```python
sort="downloads"
```

---

# Integración con Hugging Face

Intenté utilizar modelos de Hugging Face con:

```python
HuggingFacePipeline
```

Inicialmente probé:
- flan-t5-base,
- text2text-generation.

Pero aparecieron varios errores de compatibilidad.

---

# Problemas con transformers

Aparecieron errores como:

```python
KeyError: Unknown task text2text-generation
```

y también problemas relacionados con:
- ChatHuggingFace,
- chat_template,
- modelos incompatibles.

La solución fue:
- actualizar transformers,
- usar GPT2,
- utilizar `text-generation`,
- y evitar herramientas de chat más complejas.

---

# Uso de GPT2

Finalmente utilicé:

```python
pipeline(
    "text-generation",
    model="gpt2"
)
```

Esto permitió ejecutar ejemplos de manera más estable en mi entorno.

---

# Agentic RAG final

Para la integración final construí un agente simple usando:
- LangGraph,
- StateGraph,
- tools,
- routing.

El estado utilizado fue:

```python
class AgentState(TypedDict):
    question: str
    answer: str
```

El agente decidía:
- qué tool usar,
- según la pregunta del usuario.

Ejemplo:

```python
if "marie curie" in question:
```

o:

```python
elif "weather" in question:
```

---

# Flujo del agente

El flujo final fue:

1. recibir pregunta,
2. analizar pregunta,
3. decidir herramienta,
4. ejecutar tool,
5. devolver respuesta.

El grafo fue construido usando:

```python
StateGraph
```

y ejecutado con:

```python
graph.invoke()
```

---

# Diferencias respecto al curso original

El curso original utiliza:
- GPT-4o,
- modelos más grandes,
- tool calling avanzado,
- async workflows,
- APIs pagas.

Sin embargo, mi entorno presentó varios problemas de compatibilidad relacionados con:
- Windows,
- Jupyter,
- async,
- modelos HF,
- versiones de librerías.

Por eso adapté algunos ejemplos para que funcionaran localmente manteniendo:
- la arquitectura,
- los conceptos,
- y la lógica principal del curso.

---

# Lo que aprendí

- Cómo funciona Retrieval Augmented Generation.
- Cómo construir tools con LangChain.
- Cómo usar retrieval con BM25.
- Cómo integrar herramientas externas.
- Cómo usar LangGraph para crear agentes.
- Cómo manejar estados y flujos.
- Cómo adaptar notebooks cuando existen incompatibilidades de entorno.

---

# Conclusión

Esta unidad me ayudó a entender cómo construir sistemas Agentic RAG usando:
- retrieval,
- herramientas,
- agentes,
- y workflows.

También entendí que los agentes modernos no dependen únicamente de modelos de lenguaje, sino de la combinación entre:
- herramientas,
- memoria,
- retrieval,
- y control del flujo.

Finalmente logré construir una versión funcional de Alfred utilizando LangGraph, tools y retrieval adaptados a mi entorno local.