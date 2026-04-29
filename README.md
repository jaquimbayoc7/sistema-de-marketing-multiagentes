# Sistema de Marketing Multiagentes

Aplicación web que genera propuestas comerciales de marketing personalizadas usando una cadena de **4 agentes especializados** con LangGraph y Claude (Anthropic). El resultado se puede descargar en formato `.md` y `.pdf`.

---

## Demo

![Interfaz Streamlit](agente-marketing-multiagente-langgraph.html)

---

## Arquitectura de Agentes

```
                    MarketingProposalState (estado compartido)
                              │
              ┌───────────────▼───────────────┐
              │        Agente 1               │
              │    Analista de Mercado        │
              │  Framework PEST + Pain-Gain   │
              └───────────────┬───────────────┘
                              │
              ┌───────────────▼───────────────┐
              │        Agente 2               │
              │   Estratega de Marca          │
              │  Messaging Hierarchy Canvas   │
              └───────────────┬───────────────┘
                              │
              ┌───────────────▼───────────────┐
              │        Agente 3               │
              │    Redactor Comercial         │
              │   Propuesta draft completa    │
              └───────────────┬───────────────┘
                              │
              ┌───────────────▼───────────────┐
              │        Agente 4               │
              │      Editor Senior            │
              │   Revisión y propuesta final  │
              └───────────────┴───────────────┘
```

| Agente | Rol | Framework |
|--------|-----|-----------|
| `agent_market_analyst` | Analiza el cliente, su mercado, pain points y oportunidades | PEST + Pain-Gain-Fear |
| `agent_brand_strategist` | Define mensajes clave y propuesta de valor | Messaging Hierarchy Canvas |
| `agent_proposal_writer` | Redacta la propuesta comercial completa | Copywriting B2B |
| `agent_senior_editor` | Revisa, ajusta y entrega la versión final | Editorial review |

---

## Stack Tecnológico

| Capa | Tecnología |
|------|-----------|
| UI / Frontend | [Streamlit](https://streamlit.io/) |
| Orquestación de agentes | [LangGraph](https://github.com/langchain-ai/langgraph) |
| LLM | Claude `claude-haiku-4-5-20251001` via `langchain-anthropic` |
| Generación de PDF | [ReportLab](https://www.reportlab.com/) |
| Gestión de variables de entorno | `python-dotenv` |
| Runtime | Python 3.10+ |

---

## Requisitos Previos

- Python **3.10** o superior
- Una API Key de [Anthropic](https://console.anthropic.com/)
- `pip` o `pip3`

---

## Instalación

### 1. Clonar el repositorio

```bash
git clone https://github.com/jaquimbayoc7/sistema-de-marketing-multiagentes.git
cd sistema-de-marketing-multiagentes
```

### 2. Crear y activar un entorno virtual

```bash
# Linux / macOS
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

### 4. Configurar variables de entorno

Crea un archivo `.env` en la raíz del proyecto con el siguiente contenido:

```env
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxxxxxxxxxxxxx
```

> También puedes ingresar la API Key directamente en la interfaz de la aplicación sin necesidad de crear el archivo `.env`.

---

## Uso

```bash
streamlit run app.py
```

La aplicación se abrirá automáticamente en `http://localhost:8501`.

### Pasos en la interfaz

1. Ingresa (o confirma) tu **API Key de Anthropic** en la barra lateral.
2. Completa los datos del **cliente**: nombre, empresa, industria y necesidad de marketing.
3. Define el **público objetivo** y el **tipo de servicio**.
4. Agrega los datos de tu **empresa** (remitente) y el rango de presupuesto.
5. Haz clic en **"Generar Propuesta"**.
6. Los 4 agentes procesan la información en cadena.
7. Descarga la propuesta en **Markdown** o **PDF**.

---

## Estructura del Proyecto

```
02-session/
├── app.py                                   # Aplicación principal (agentes + UI Streamlit)
├── requirements.txt                         # Dependencias del proyecto
├── CLAUDE.md                                # Documentación de arquitectura para Claude
├── agente-marketing-multiagente-langgraph.html  # Demo / documentación visual
├── .gitignore
└── README.md
```

---

## Variables de Entorno

| Variable | Descripción | Obligatoria |
|----------|-------------|-------------|
| `ANTHROPIC_API_KEY` | API Key de Anthropic para acceder a Claude | Solo si no se ingresa en la UI |

---

## Exportación de la Propuesta

La propuesta generada se puede descargar en dos formatos:

- **Markdown (`.md`)** — texto con formato listo para editar.
- **PDF (`.pdf`)** — documento profesional con estilos corporativos generado con ReportLab.

---

## Licencia

MIT
