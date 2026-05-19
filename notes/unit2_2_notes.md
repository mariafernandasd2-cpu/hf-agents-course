# Unit 2.2 - LlamaIndex

## Introducción a LlamaIndex

En esta unidad aprendí que LlamaIndex es un framework enfocado en crear agentes con modelos de lenguaje utilizando workflows, tools, componentes e índices. A diferencia de smolagents, LlamaIndex tiene una estructura más organizada y está pensado para proyectos más grandes o aplicaciones donde se necesite manejar documentos y flujos complejos.

Los conceptos principales vistos fueron:

- Components
- Tools
- Agents
- Workflows

También aprendí que LlamaIndex tiene integración con muchas herramientas externas mediante LlamaHub.

---

# LlamaHub

LlamaHub funciona como un catálogo de integraciones para LlamaIndex. Ahí se pueden encontrar modelos, embeddings, tools y otros componentes ya preparados.

La instalación normalmente sigue esta estructura:

```bash
pip install llama-index-{tipo}-{framework}
```

Ejemplo usado en la unidad:

```bash
pip install llama-index-llms-huggingface-api
pip install llama-index-embeddings-huggingface
```

---

# Integración con Hugging Face

Para conectar modelos desde Hugging Face usamos:

```python
from llama_index.llms.huggingface_api import HuggingFaceInferenceAPI
```

El modelo utilizado fue:

```python
Qwen/Qwen2.5-Coder-32B-Instruct
```

La configuración quedó así:

```python
llm = HuggingFaceInferenceAPI(
    model_name="Qwen/Qwen2.5-Coder-32B-Instruct",
    token=hf_token,
    provider="auto"
)
```

---

# Problemas encontrados y soluciones

## Error 1: No module named 'llama_index'

Inicialmente el notebook no reconocía llama_index porque la librería no estaba instalada.

Solución:

```bash
pip install llama-index
```

También fue necesario instalar:

```bash
pip install llama-index-llms-huggingface-api
pip install llama-index-embeddings-huggingface
```

---

## Error 2: API key de OpenAI

LlamaIndex intentaba usar OpenAI por defecto para embeddings y aparecía el siguiente error:

```python
No API key found for OpenAI
```

La solución fue utilizar embeddings de Hugging Face en vez de OpenAI.

---

## Error 3: Problemas con async y workflows

En el notebook de agents aparecieron varios errores relacionados con asyncio y workflows:

- await wasn't used with future
- Event loop stopped before Future completed
- Cannot send a request, as the client has been closed

El problema venía de la combinación entre:

- VSCode
- Jupyter notebooks
- Windows
- workflows async de LlamaIndex

La solución práctica fue:

- reiniciar kernels
- crear notebooks nuevos
- evitar reutilizar event loops dañados
- usar `.run()` directamente

Aun así algunos workflows siguieron generando errores internos de asyncio.

---

# Components

Aprendí que los components son los bloques básicos de LlamaIndex.

Por ejemplo:

- modelos
- embeddings
- documentos
- índices

También usamos:

```python
VectorStoreIndex
```

para indexar documentos.

Ejemplo:

```python
index = VectorStoreIndex.from_documents(documents)
```

---

# Tools

Las tools permiten que los agentes ejecuten funciones específicas.

Usamos:

```python
FunctionTool
```

Ejemplo:

```python
def multiply(a: int, b: int):
    return a * b
```

y luego:

```python
tool = FunctionTool.from_defaults(fn=multiply)
```

---

# Agents

Creamos un agente usando:

```python
AgentWorkflow.from_tools_or_functions()
```

El agente utilizó una tool matemática simple y un modelo de Hugging Face.

Código principal:

```python
agent = AgentWorkflow.from_tools_or_functions(
    [tool],
    llm=llm
)
```

Luego se ejecutó:

```python
response = agent.run("What is 5 times 8?")
```

El resultado devolvió un WorkflowHandler debido al manejo interno async de LlamaIndex en Jupyter.

---

# Manejo del token

No dejé el token directamente en el notebook porque quedaría expuesto en GitHub.

Se utilizó un archivo `.env` con:

```text
HF_TOKEN=mi_token
```

y luego:

```python
from dotenv import load_dotenv
import os

load_dotenv()

hf_token = os.getenv("HF_TOKEN")
```

Además el archivo `.env` quedó agregado al `.gitignore`.

---

# Diferencias entre smolagents y LlamaIndex

## smolagents

- más simple
- más rápido de probar
- mejor para ejemplos pequeños
- usa code agents fácilmente

## LlamaIndex

- más estructurado
- pensado para workflows grandes
- mejor integración con documentos e índices
- más complejo de configurar

---

# Conclusiones

LlamaIndex es más potente y estructurado que smolagents, pero también más complicado de configurar. La parte más difícil fue el manejo de workflows asíncronos en Jupyter.

También entendí la importancia de manejar correctamente:

- tokens
- embeddings
- workflows async
- configuración de modelos

Finalmente logré crear tools, components y agentes usando LlamaIndex y Hugging Face.