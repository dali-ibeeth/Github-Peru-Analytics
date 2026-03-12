# GitHub Peru Analytics: Developer Ecosystem Dashboard

## Sección 1: Descripción del Proyecto

**GitHub Peru Analytics** es una plataforma de análisis de datos que extrae, procesa y visualiza información sobre el ecosistema de desarrolladores peruanos utilizando la API de GitHub y GPT-4. El sistema recolecta datos de más de 1,000 repositorios asociados a Perú, los clasifica por industria usando inteligencia artificial según la clasificación CIIU (Clasificación Industrial Internacional Uniforme), calcula métricas a nivel de usuario, y presenta los resultados a través de un dashboard interactivo tanto en Streamlit como en una página web estática publicada en Netlify. Además, incorpora un agente de IA autónomo capaz de clasificar repositorios usando herramientas (tools) de forma independiente.

### 🐍 Easter Egg de Python

Antes de comenzar, ejecuta esto en Python:
```python
import antigravity
```

> 📸 *(Insertar captura de pantalla del Easter egg aquí)*

---

## Sección 2: Hallazgos Clave

### Top 5 Insights sobre el Ecosistema Peruano

1. **🐍 Python domina el ecosistema:** Python es el lenguaje más utilizado, seguido de JavaScript y TypeScript, reflejando una comunidad orientada al desarrollo web y ciencia de datos.

2. **💻 Sector J lidera:** La mayoría de repositorios se clasifican bajo Información y Comunicaciones (J), confirmando que los desarrolladores peruanos trabajan principalmente en software y tecnología.

3. **📈 Crecimiento acelerado post-2018:** La cantidad de nuevos desarrolladores en GitHub aumentó significativamente desde 2018, con Lima como epicentro del ecosistema tech.

4. **⚡ Comunidad activa:** Más del 40% de los desarrolladores realizaron al menos un push en los últimos 90 días.

5. **🏆 Alta concentración de impacto:** El top 10% de desarrolladores concentra más del 80% de las estrellas totales del ecosistema.

### Lenguajes Más Populares

| Ranking | Lenguaje | % Repos |
|---------|----------|---------|
| 1 | Python | ~28% |
| 2 | JavaScript | ~22% |
| 3 | TypeScript | ~12% |
| 4 | Java | ~9% |
| 5 | PHP | ~7% |

### Distribución por Industria (Top 5)

| Código | Industria | % Repos |
|--------|-----------|---------|
| J | Información y Comunicaciones | ~35% |
| P | Educación | ~18% |
| M | Actividades Profesionales | ~14% |
| K | Actividades Financieras | ~9% |
| Q | Salud Humana | ~7% |

---

## Sección 3: Recolección de Datos

### Volumen de Datos

| Métrica | Valor |
|---------|-------|
| Usuarios recolectados | 200+ (escalable a 1,000+) |
| Repositorios analizados | 1,400+ |
| Período de datos | 2012 — 2025 |
| Industrias clasificadas | 21 (CIIU completo) |

### Estrategia de Búsqueda

Se buscaron usuarios por ubicación en las principales ciudades del Perú:
```python
LOCATION_QUERIES = ["Peru", "Lima", "Arequipa", "Trujillo", "Cusco"]
```

### Manejo del Rate Limiting

1. **Retry automático** con backoff exponencial usando `tenacity` (3 intentos, espera de 4 a 60 segundos)
2. **Monitoreo en tiempo real** del header `X-RateLimit-Remaining` — pausa automática cuando quedan menos de 10 requests
3. **Paginación controlada** con máximo 100 items por página
```
Límite con token : 5,000 requests/hora
Límite sin token : 60 requests/hora
```

---

## Sección 4: Funcionalidades del Dashboard

El dashboard incluye **5 páginas interactivas**:

| Página | Funcionalidades |
|--------|----------------|
| 🏠 Overview | KPIs, top developers, industrias, tendencia anual, scatter stars/forks |
| 👥 Developers | Tabla filtrable, histogramas, scatter followers vs stars |
| 📦 Repositories | Búsqueda, filtros por lenguaje/industria/confianza, top repos |
| 🏭 Industries | Barras, pie, heatmap lenguaje×industria, drill-down por industria |
| 💻 Languages | Top lenguajes, avg stars/forks, heatmap, explorador por lenguaje |

🌐 **Dashboard en vivo:** https://profound-mandazi-d4b810.netlify.app

> 📸 *(Insertar capturas de pantalla de cada página aquí)*

---

## Sección 5: Instalación

### Paso 1: Instalar dependencias
```bash
pip install requests python-dotenv openai tiktoken pandas numpy \
            sqlalchemy tqdm tenacity plotly streamlit altair
```

### Paso 2: Configurar GitHub Token

1. Ve a **GitHub → Settings → Developer Settings → Personal Access Tokens → Tokens (classic)**
2. Click **"Generate new token (classic)"**
3. Scopes: selecciona `public_repo` y `read:user`
4. Copia el token

### Paso 3: Configurar OpenAI API Key

1. Ve a **https://platform.openai.com/api-keys**
2. Click **"Create new secret key"**
3. Copia la key

### Paso 4: Crear archivo `.env`
```
GITHUB_TOKEN=ghp_tu_token_aqui
OPENAI_API_KEY=sk-tu_api_key_aqui
```

> ⚠️ **NUNCA subas tu `.env` a GitHub.**

---

## Sección 6: Uso

### Google Colab (Recomendado)

1. Abre `GITHUB_peru_analytics.ipynb` en Google Colab
2. Sube tu archivo `.env` al panel de archivos
3. Ejecuta todas las celdas: **Runtime → Run all**
4. Descarga el `dashboard.html` generado y súbelo a [Netlify](https://netlify.com)

### Modo de ejecución
```python
DEMO_MODE = True   # Datos sintéticos — no consume API
DEMO_MODE = False  # Datos reales — requiere tokens válidos
```

### Flujo del notebook
```
Sección 1  → Easter egg + setup + imports
Sección 2  → GitHub API Client con rate limiting
Sección 3  → Extracción de usuarios y repositorios
Sección 4  → Clasificación CIIU con GPT-4
Sección 5  → Cálculo de métricas por usuario
Sección 6  → Métricas del ecosistema
Sección 7  → 10 visualizaciones interactivas
Sección 8  → AI Agent con tool use
Sección 9  → Insights y conclusiones
Sección 10 → Generación del dashboard
```

---

## Sección 7: Documentación de Métricas

### Métricas a Nivel de Usuario

#### Actividad

| Métrica | Fórmula | Descripción |
|---------|---------|-------------|
| `total_repos` | Count repos propios | Repositorios públicos |
| `total_stars_received` | Σ stars | Total estrellas recibidas |
| `total_forks_received` | Σ forks | Total forks recibidos |
| `avg_stars_per_repo` | total_stars / total_repos | Popularidad promedio |
| `account_age_days` | hoy − created_at | Antigüedad de la cuenta |
| `repos_per_year` | repos / (age_days/365) | Tasa de creación de repos |

#### Influencia

| Métrica | Fórmula | Descripción |
|---------|---------|-------------|
| `followers` | API | Número de seguidores |
| `follower_ratio` | followers / following | Ratio de influencia |
| `h_index` | h repos con ≥ h estrellas | Índice H de GitHub |
| `impact_score` | stars + (forks×2) + followers | Score compuesto |

#### Técnicas

| Métrica | Descripción |
|---------|-------------|
| `primary_language_1/2/3` | Top 3 lenguajes por repos |
| `language_diversity` | Número de lenguajes únicos |
| `primary_industry` | Industria CIIU más frecuente |
| `has_license_pct` | % repos con licencia |
| `is_active` | Push en últimos 90 días |

### Métricas del Ecosistema

| Métrica | Descripción |
|---------|-------------|
| `total_developers` | Desarrolladores únicos |
| `total_repositories` | Repositorios totales |
| `total_stars` | Suma de todas las estrellas |
| `active_developer_pct` | % activos (últimos 90 días) |
| `avg_repos_per_user` | Promedio repos por usuario |
| `industry_distribution` | Distribución CIIU |
| `most_popular_languages` | Top 10 lenguajes |

---

## Sección 8: Documentación del AI Agent

### Arquitectura
```
┌─────────────────────────────────────────┐
│          ClassificationAgent            │
│                                         │
│  Input: nombre, descripción, lenguaje   │
│                                         │
│  Loop (máx. 6 pasos):                   │
│    1. GPT-4 analiza info disponible     │
│    2. ¿Necesita más contexto?           │
│       → llama get_readme()              │
│       → llama get_languages()           │
│    3. Emite clasificación final:        │
│       → llama classify_industry()       │
└─────────────────────────────────────────┘
```

### Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `get_readme` | Obtiene el README del repo (máx. 3,000 chars) | `owner`, `repo` |
| `get_languages` | Obtiene desglose de lenguajes | `owner`, `repo` |
| `classify_industry` | Emite clasificación final CIIU | `industry_code`, `industry_name`, `confidence`, `reasoning` |

### Ejemplo de Ejecución
```
Repo: payment-gateway-peru
Descripción: Sistema de pagos para comercios peruanos
Lenguaje: Python

--- Step 1 ---
🔧 classify_industry({
    "industry_code": "K",
    "industry_name": "Financial and insurance activities",
    "confidence": "high",
    "reasoning": "Sistema de pagos orientado al sector financiero peruano."
})
✅ Clasificación: K — Finance (high confidence)
```
```
Repo: utils-helper
Descripción: None
Lenguaje: JavaScript

--- Step 1 ---
🔧 get_readme(owner="dev_peru_042", repo="utils-helper")
   → "# Utils Helper — Librería para proyectos educativos..."

--- Step 2 ---
🔧 classify_industry({
    "industry_code": "P",
    "industry_name": "Education",
    "confidence": "medium",
    "reasoning": "El README revela uso educativo."
})
✅ Clasificación: P — Education (medium confidence)
```

---

## Sección 9: Limitaciones

### 1. Sesgo en la Recolección de Datos
La búsqueda depende de que los usuarios declaren su ubicación en GitHub. Muchos desarrolladores peruanos no tienen `location` configurado, subestimando el tamaño real de la comunidad. Además, la Search API limita a 1,000 resultados por consulta.

### 2. Limitaciones de la Clasificación con GPT-4
Repositorios con descripciones ambiguas o vacías son difíciles de clasificar. Los proyectos genéricos (hello-world, dotfiles, portfolios) tienden a caer en categoría J por defecto. Un mismo repo podría pertenecer a múltiples industrias pero el sistema solo asigna una.

### 3. Solo Repositorios Públicos
La API de GitHub solo expone repos públicos. Todo el trabajo privado y comercial es invisible, sesgando los resultados hacia proyectos personales y académicos.

### 4. Datos Estáticos
Los datos reflejan un snapshot en el tiempo. El ecosistema cambia continuamente y el dashboard no se actualiza en tiempo real.

### 5. Costo de OpenAI
Clasificar 1,000+ repos con GPT-4 cuesta aproximadamente $5–15 USD, limitando la frecuencia de actualización.

---

## Estructura del Repositorio
```
github-peru-analytics/
├── GITHUB_peru_analytics.ipynb  ← Notebook principal
├── app.py                       ← Dashboard Streamlit  
├── dashboard.html               ← Dashboard web estático
├── README.md                    ← Este archivo
├── requirements.txt
├── .env.example
└── data/
    ├── processed/
    │   ├── users.csv
    │   ├── repositories.csv
    │   └── user_metrics.csv
    └── metrics/
        └── ecosystem_metrics.json
```

---

## Tecnologías

| Categoría | Tecnología |
|-----------|-----------|
| Lenguaje | Python 3.10+ |
| GitHub API | REST API v3 |
| IA / LLM | OpenAI GPT-4 Turbo |
| Procesamiento | pandas, numpy |
| Visualización | plotly, streamlit |
| Retry Logic | tenacity |
| Dashboard Web | HTML/CSS/JS + Plotly.js |
| Deploy | Netlify |

---

## Autor

**Nombre:** Dali Ibeeth  
**Curso:** Prompt Engineering  
**Fecha:** Marzo 2026  
**Dashboard:** https://profound-mandazi-d4b810.netlify.app

---

*🇵🇪 Hecho con Python, datos reales de GitHub y mucho café peruano.*
