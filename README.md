# 🤖 Agentes de IA - Implementación Personal (Inmersión 2026)

**Autor:** Gerardo ([@BarbonRecargado](https://github.com/BarbonRecargado))  
**Curso:** Inmersión de Inteligencia Artificial 2026 - Alura  
**Estado:** ✅ Completado

---

## 📖 Descripción

Este repositorio documenta mi implementación personal de los conceptos aprendidos durante la Inmersión de IA 2026.

No es una copia del material del curso: es una solución construida desde cero, enfrentando errores reales, cambios de versiones y limitaciones de entorno.

El proyecto combina dos enfoques complementarios:
- Un **agente de IA en n8n** con memoria y acceso a información en tiempo real
- Un **sistema RAG en Python (Google Colab)** basado en documentos PDF reales

---

## 🏗️ Arquitectura del Proyecto

### Agente en n8n
Un agente conversacional dual construido visualmente con:
- **Gemini de Google** como modelo de lenguaje
- **Memoria simple** para mantener contexto de conversación
- **Tavily** como herramienta de búsqueda web general en tiempo real
- **Noticias News API** como herramienta especializada en noticias recientes en español, con autenticación por credencial y parámetros fijos (idioma, cantidad, orden por fecha)
- Un **mensaje del sistema** que le indica al agente cuándo usar cada herramienta: News API para noticias y actualidad, Tavily para cualquier otro tema

El flujo (JSON exportado) está disponible en [`n8n/agente-noticias-final.json`](n8n/agente-noticias-final.json).

### Cuaderno Python (Google Colab)
Un sistema RAG completo con grafo de decisión construido con LangGraph:

```
[START] → [Agente]
           ├── RAG → [Buscar en PDFs] → [Generar Markdown] → END
           └── Web → [Buscar en Web] → [Generar Markdown] → END
```

---

## 🛠️ Tecnologías principales utilizadas en la implementación:

### 1. Librería deprecada de Google
El curso utilizaba `google-generativeai`, actualmente deprecada. Migré a `google-genai`, el SDK oficial vigente, ajustando imports y métodos.

### 2. Modelos no disponibles
Modelos como `gemini-1.5-flash` y `text-embedding-004` devolvían error 404. Consulté los modelos disponibles mediante `client.models.list()` y adapté la implementación a `gemini-2.0-flash` y `gemini-embedding-001`.

---

## ⚔️ Obstáculos Superados

Esta implementación no fue en un ambiente controlado. Estos son los problemas reales que encontré y resolví:

### 1. Librería deprecada de Google
El curso usaba `google-generativeai` (deprecada). Migré a `google-genai`, el SDK oficial actual.

### 2. Modelos no disponibles
`gemini-1.5-flash` y `text-embedding-004` daban error 404. Identifiqué los modelos disponibles para mi cuenta con `client.models.list()` y usé `gemini-embedding-001` y `gemini-2.0-flash`.

### 3. SerpAPI sin acceso
El curso usaba SerpAPI para búsqueda web, pero no pude verificar mi cuenta. Reemplacé por **Tavily**, que ya tenía funcionando en mi nodo de n8n, manteniendo la misma funcionalidad.

### 4. Variables no definidas entre celdas
Aprendí que en Google Colab el orden de ejecución de las celdas es crítico. Reorganicé el flujo para que cada variable exista antes de ser llamada.

---

## 📁 Estructura del Repositorio

```
📦 Implementacion_Personal_Agentes_IA_Inmersion_2026
 ┣ 📓 Implementacion_Personal_Agentes_IA_Inmersion_2026.ipynb
 ┣ 📁 n8n/
 ┃ ┗ agente-noticias-final.json
 ┣ 📸 img/
 ┃ ┣ nodo_n8n.png
 ┃ ┗ grafo_langgraph.png
 ┗ 📄 README.md
```

---

## 🚀 Cómo Reproducir

1. Abre el cuaderno en Google Colab o en VS Code u otro editor de código
2. Agrega tu `GOOGLE_API_KEY` y `TAVILY_API_KEY` en los Secrets de Colab (ícono 🔑)
3. Ejecuta las celdas en orden de arriba hacia abajo
4. Sube tus PDFs cuando el botón de carga aparezca
5. (Opcional) Ajusta los modelos según disponibilidad en tu cuenta de Gemini

---

## 💡 Aprendizajes Clave

- La diferencia entre un ambiente controlado y el mundo real es enorme
- Saber **leer un error** y darle contexto preciso a una IA es una habilidad fundamental
- La documentación oficial siempre gana sobre tutoriales desactualizados
- `client.models.list()` es tu mejor amigo cuando un modelo da 404
- Adaptación a cambios de SDKs y librerías en tiempo real
- Integración de múltiples herramientas (n8n + Python + APIs externas)
- Diseño de flujos de decisión con LangGraph
- Resolución de errores en entornos no controlados


---

## 👤 Sobre el Autor

Gerardo, 62 años, Guatemala. Mensajero de alto rendimiento y ahora también explorador del mundo de la Inteligencia Artificial. Prueba de que nunca es tarde para aprender tecnología cuando la curiosidad y la perseverancia están presentes.

## 🎥 Video Demostración

Demostración del agente de n8n respondiendo una consulta de noticias (usando News API) y una consulta general (usando Tavily):

🔗 [Ver video en Google Drive](https://drive.google.com/file/d/1zu9CqVfg_1_eJXsu09noqkVk3hUNapsC/view?usp=drive_link)

---

*Construido con ☕, perseverancia y muchos errores 404 superados.*
