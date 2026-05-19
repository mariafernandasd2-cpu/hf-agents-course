# Unit 2.3 - LangGraph

## Introducción

En esta unidad trabajé con LangGraph, un framework de LangChain diseñado para construir aplicaciones con agentes y flujos controlados. A diferencia de smolagents, donde el agente tiene mucha libertad, LangGraph permite definir exactamente qué pasos seguir y cómo se conectan entre sí.

La idea principal de LangGraph es construir un flujo usando:
- States
- Nodes
- Edges
- Conditional edges

Todo funciona como un grafo dirigido donde cada nodo representa una acción o proceso.

---

# Diferencia entre LangGraph y smolagents

smolagents:
- Más flexible
- Los agentes pueden improvisar más
- Pueden ejecutar varias herramientas libremente
- Menos control sobre el flujo

LangGraph:
- Mucho más controlado
- El flujo se diseña manualmente
- Ideal para aplicaciones productivas
- Más fácil de depurar y mantener

Entendí que LangGraph es mejor cuando se necesita que el sistema siga pasos específicos y no haga cosas inesperadas.

---

# Conceptos importantes

## State

El State guarda toda la información que viaja entre nodos.

Ejemplo:

```python
class State(TypedDict):
    graph_state: str
```

El estado se actualiza en cada nodo.

---

## Nodes

Los nodos son funciones de Python.

Cada nodo:
- recibe el estado,
- hace una acción,
- devuelve cambios al estado.

Ejemplo:

```python
def node_1(state):
    return {
        "graph_state": state["graph_state"] + " I am"
    }
```

---

## Edges

Los edges conectan nodos.

Ejemplo:

```python
builder.add_edge(START, "node_1")
```

Esto significa:
START → node_1

---

## Conditional edges

Permiten decidir dinámicamente cuál nodo ejecutar.

Ejemplo:

```python
builder.add_conditional_edges(
    "node_1",
    decide_mood
)
```

Dependiendo del resultado:
- puede ir a node_2
- o a node_3

---

# Primer grafo simple

Construí un grafo básico donde:
1. Se inicia el flujo
2. Se ejecuta node_1
3. Se decide aleatoriamente entre:
   - node_2
   - node_3
4. El flujo termina

Ejemplo del resultado:

```python
---Node 1---
---Node 2---
{'graph_state': 'Hi, this is Maria. I am happy!'}
```

o también:

```python
---Node 1---
---Node 3---
{'graph_state': 'Hi, this is Maria. I am sad!'}
```

---

# Proyecto de clasificación de emails

También hice un ejemplo más realista usando un grafo para clasificar correos.

El flujo fue:
1. Leer email
2. Clasificar email
3. Decidir si es spam o legítimo
4. Ejecutar el nodo correspondiente

El state utilizado fue:

```python
class EmailState(TypedDict):
    email: str
    category: str
```

La clasificación se hacía revisando si el correo contenía "win money".

Si aparecía:
- categoría = spam

Si no:
- categoría = legitimate

---

# Uso de HuggingFacePipeline

Probé integrar modelos de Hugging Face usando:

```python
from transformers import pipeline
from langchain_huggingface import HuggingFacePipeline
```

Inicialmente intenté usar:
- flan-t5-base
- text2text-generation

pero tuve varios errores de compatibilidad.

---

# Errores encontrados

## Error con text2text-generation

Apareció:

```python
KeyError: Unknown task text2text-generation
```

La solución fue:
- actualizar transformers
- usar gpt2
- cambiar a text-generation

---

## Error con ChatHuggingFace

También apareció:

```python
ValueError: tokenizer.chat_template is not set
```

Esto pasó porque GPT2 no es un modelo tipo chat moderno.

La solución fue:
- eliminar ChatHuggingFace
- usar directamente:

```python
llm.invoke()
```

---

# Lo que aprendí

- LangGraph permite controlar completamente el flujo de una aplicación.
- Los estados son fundamentales porque almacenan la información entre nodos.
- Los conditional edges permiten construir lógica dinámica.
- No todos los modelos de Hugging Face funcionan igual con LangChain.
- GPT2 funciona mejor para pruebas simples locales.
- Muchas veces los ejemplos oficiales están pensados para GPT-4o y requieren adaptaciones cuando se trabaja localmente.

---

# Conclusión

LangGraph me pareció mucho más estructurado que smolagents. Aunque requiere escribir más lógica manualmente, permite crear aplicaciones más organizadas y controladas.

También entendí que en proyectos reales es importante controlar:
- el flujo,
- las decisiones,
- los estados,
- y las transiciones entre procesos.

Esta unidad me ayudó a entender mejor cómo funcionan internamente los agentes y cómo se pueden construir sistemas multi-step usando grafos.