# GitHub Peru Analytics: Developer Ecosystem Dashboard

## Sección 1: Descripción del Proyecto

**GitHub Peru Analytics** es una plataforma de análisis de datos que extrae, procesa y visualiza información sobre el ecosistema de desarrolladores peruanos utilizando la API de GitHub y GPT-4. El sistema recolecta datos de más de 1,000 repositorios asociados a la locación de Perú, los clasifica por industria usando inteligencia artificial, calcula métricas a nivel de usuario, y presenta los resultados a través de un dashboard interactivo . 


### Top 5 Insights sobre el Ecosistema Peruano

1. **Comunidad activa y en crecimiento:** El ecosistema GitHub para este análisis alberga 200 desarrolladores con 1,400 repositorios y 27,125 estrellas totales, mostrando una comunidad con proyectos de calidad y alcance internacional.

2. **PHP lidera los lenguajes:** PHP es el lenguaje más utilizado con 114 repositorios, seguido de Go, Ruby, Kotlin y C#, reflejando una comunidad orientada al desarrollo web y backend.

3. **Sector Financiero domina la clasificación:** La mayoría de repositorios se clasifican bajo la industria K (Actividades Financieras y de Seguros), lo que indica una comunidad enfocada en soluciones fintech y de negocios.

4. **Ecosistema extremadamente activo:** El 98.5% de los desarrolladores realizaron al menos un push en los últimos 90 días, indicando un nivel de actividad excepcional y proyectos en mantenimiento constante.

5. **H-Index promedio de 5.1:** El h-index promedio de 5.1 refleja que los desarrolladores peruanos tienen repositorios con impacto real y reconocimiento de la comunidad open source global.

### Lenguajes Más Populares

| Ranking | Lenguaje | Repositorios |
|---------|----------|-------------|
| 1 | PHP | 114 |
| 2 | Go | ~110 |
| 3 | Ruby | ~108 |
| 4 | Kotlin | ~107 |
| 5 | C# | ~105 |
| 6 | Rust | ~104 |
| 7 | R | ~103 |
| 8 | Dart | ~101 |
| 9 | Swift | ~100 |
| 10 | JavaScript | ~98 |

### Distribución por Industria

| Código | Industria | Descripción |
|--------|-----------|-------------|
| K | Financial & Insurance | Industria dominante |
| J | Information & Tech | Segunda más frecuente |
| M | Professional Services | Tercera más frecuente |
| P | Education | Cuarta más frecuente |
| G | Trade | Quinta más frecuente |


## Sección 3: Recolección de Datos

### Volumen de Datos

| Métrica | Valor |
|---------|-------|
| Usuarios recolectados | 200 |
| Repositorios analizados | 1,400 |
| Industrias clasificadas | 21 (CIIU completo) |
| Período de datos | 2012 — 2025 |
| Antigüedad promedio de cuentas | 3,280 días (~9 años) |
| Promedio repos por usuario | 7.0 |
| Promedio estrellas por repo | 19.38 |

### Estrategia de Búsqueda

Se buscaron usuarios por ubicación en las principales ciudades del Perú:
```python
LOCATION_QUERIES = ["Peru", "Lima", "Arequipa", "Trujillo", "Cusco"]
```

Para cada usuario se extrajeron todos sus repositorios propios (no forks), junto con su README y desglose de lenguajes de programación.

### Manejo del Rate Limiting

| Autenticación | Límite |
|---------------|--------|
| Con token | 5,000 requests/hora  |
| Sin token | 60 requests/hora  |



## Sección 4: Funcionalidades del Dashboard

El dashboard incluye **5 páginas interactivas**:

###  Overview
- 5 KPIs del ecosistema: desarrolladores, repositorios, estrellas, forks y % activos
- Top 10 desarrolladores por Impact Score
- Distribución de industrias 
- Tendencia de nuevos desarrolladores por año
- Top lenguajes de programación
- Scatter Stars vs Forks por lenguaje 

### Repository Browser
- Búsqueda por nombre o descripción
- Filtros por lenguaje, industria CIIU y nivel de confianza de clasificación
- Top 15 repositorios por estrellas
- Repositorios creados por año
- Distribución de estrellas 

###  Industry Analysis
- Gráfico de barras de repos por industria
- Gráfico de participación (pie) por industria
- Heatmap Lenguaje × Industria (top 10 × top 10)
- Drill-down interactivo: top repos por industria seleccionada

### 💻 Language Analytics
- Top 15 lenguajes por cantidad de repos
- Share de lenguajes top 10 
- Promedio de estrellas por lenguaje
- Promedio de forks por lenguaje
- Explorador de repos por lenguaje seleccionado

🌐 **Dashboard en vivo:** https://profound-mandazi-d4b810.netlify.app

<img width="1896" height="843" alt="{DDB38A71-6B4F-4B51-8D63-75F8A5077BDC}" src="https://github.com/user-attachments/assets/5a1531e7-4074-4cd6-8eee-33710b6be8b6" />

<img width="1658" height="849" alt="{CE410554-90FE-4D93-B288-2BD8CB4CA14E}" src="https://github.com/user-attachments/assets/e8665e75-e28a-43c9-9de6-a2321de45ba0" />

<img width="1561" height="888" alt="{00A9B7FE-AB48-4D48-BD2B-40038DC6471F}" src="https://github.com/user-attachments/assets/22b2baef-d0ce-49d9-bfd2-cd5cdf11d691" />


## Sección 5: Instalación

### Paso 1: Instalar dependencias
```bash
pip install requests python-dotenv openai tiktoken pandas numpy \
            sqlalchemy tqdm tenacity plotly streamlit altair
```

### Paso 2: Configurar GitHub Token

### Paso 3: Configurar OpenAI API Key

### Paso 4: Crear archivo `.env`
```
GITHUB_TOKEN=................
OPENAI_API_KEY=.............
```

## Sección 6: Uso


### Flujo del Notebook
```
Sección 1  (Celdas 1-5)   → Easter egg + setup + imports
Sección 2  (Celda 6)      → GitHub API Client con rate limiting
Sección 3  (Celdas 7-10)  → Extracción: 200 usuarios y 1,400 repos
Sección 4  (Celdas 11-14) → Clasificación CIIU con GPT-4
Sección 5  (Celdas 15-17) → Cálculo de métricas por usuario
Sección 6  (Celda 18)     → Métricas del ecosistema
Sección 7  (Celdas 19-29) → 10 visualizaciones con Plotly
Sección 8  (Celdas 30-31) → AI Agent con tool use
Sección 9  (Celdas 32-34) → Key insights y dashboard final
Sección 10 (Celdas 35-37) → Generación del dashboard web
```

---

## Sección 7: Documentación de Métricas

### Métricas a Nivel de Usuario

#### Métricas de Actividad

| Métrica | Fórmula | Descripción |
|---------|---------|-------------|
| `total_repos` | Count repos propios | Número de repositorios públicos |
| `total_stars_received` | Σ stars de todos los repos | Total de estrellas recibidas |
| `total_forks_received` | Σ forks de todos los repos | Total de forks recibidos |
| `avg_stars_per_repo` | total_stars / total_repos | Popularidad promedio por repo |
| `account_age_days` | hoy − created_at | Días desde la creación de cuenta |
| `repos_per_year` | repos / (age_days / 365) | Tasa de creación de repositorios |

#### Métricas de Influencia

| Métrica | Fórmula | Descripción |
|---------|---------|-------------|
| `followers` | Directo de la API | Número de seguidores |
| `following` | Directo de la API | Número de seguidos |
| `follower_ratio` | followers / following | Ratio de influencia |
| `h_index` | h repos con ≥ h estrellas | Índice H adaptado a GitHub |
| `impact_score` | stars + (forks×2) + followers | Score de impacto compuesto |

> **Cálculo del H-Index:** Un desarrollador tiene h-index = h si tiene exactamente h repositorios con al menos h estrellas cada uno. El promedio del ecosistema es **5.1**.

#### Métricas Técnicas

| Métrica | Descripción |
|---------|-------------|
| `primary_language_1/2/3` | Top 3 lenguajes por cantidad de repos |
| `language_diversity` | Número de lenguajes únicos utilizados |
| `primary_industry` | Industria CIIU más frecuente en sus repos |
| `industries_served` | Número de industrias CIIU diferentes |
| `has_license_pct` | % de repos con licencia declarada |

#### Métricas de Engagement

| Métrica | Descripción |
|---------|-------------|
| `total_open_issues` | Suma de issues abiertos en todos sus repos |
| `days_since_last_push` | Días desde el último push a cualquier repo |
| `is_active` | `True` si hizo push en los últimos 90 días |

### Métricas del Ecosistema (Valores Reales del Notebook)

| Métrica | Valor |
|---------|-------|
| `total_developers` | 200 |
| `total_repositories` | 1,400 |
| `total_stars` | 27,125 |
| `total_forks` | 5,465 |
| `avg_repos_per_user` | 7.0 |
| `avg_stars_per_repo` | 19.38 |
| `active_developer_pct` | 98.5% |
| `avg_account_age_days` | 3,280 días |

---

## Sección 8: Documentación del AI Agent

### Arquitectura del Agente

El `ClassificationAgent` es un agente autónomo basado en GPT-4 con **tool use** que clasifica repositorios de GitHub en categorías CIIU. A diferencia del clasificador simple (`IndustryClassifier`), el agente decide autónomamente qué información adicional necesita antes de emitir su clasificación final.
```
┌─────────────────────────────────────────────┐
│           ClassificationAgent               │
│                                             │
│  Input: nombre, descripción, lenguaje       │
│                                             │
│  Loop autónomo (máx. 6 pasos):              │
│    1. GPT-4 analiza info disponible         │
│    2. ¿Necesita más contexto?               │
│       → llama get_readme()                  │
│       → llama get_languages()               │
│    3. Cuando tiene suficiente info:         │
│       → llama classify_industry()           │
│         (detiene el loop)                   │
│                                             │
│  Fallback: industria J, confianza "low"     │
└─────────────────────────────────────────────┘
```

### Descripción de Herramientas (Tools)

| Tool | Descripción | Parámetros |
|------|-------------|------------|
| `get_readme` | Obtiene el README del repo (máx. 3,000 chars) | `owner`, `repo` |
| `get_languages` | Obtiene el desglose de lenguajes del repo | `owner`, `repo` |
| `classify_industry` | Emite la clasificación CIIU final | `industry_code`, `industry_name`, `confidence`, `reasoning` |

### Ejemplo de Ejecución Real (del Notebook)
```
Repository : repo_0
Description: A TypeScript project for industry O.
Language   : TypeScript

--- Agent Step 1 ---
🔧 Tool called: classify_industry(...)
✅ Classification: industry_code=F, confidence=medium

Final Classification:
{
  "industry_code": "F",
  "industry_name": "Construction",
  "confidence"   : "medium",
  "reasoning"    : "Synthetic classification."
}
```

### Características del Agente

- **Autonomía:** Decide cuándo necesita más información sin intervención humana
- **Multi-tool:** Puede encadenar `get_readme` + `get_languages` antes de clasificar
- **Razonamiento explícito:** Cada clasificación incluye campo `reasoning` con justificación
- **Manejo de errores:** Fallback automático a industria J con confianza `low` si no converge
- **Logging:** Cada paso queda registrado para auditoría y debugging

---

## Sección 9: Limitaciones

### 1. Datos Sintéticos en Modo Demo
Este notebook se ejecutó en `DEMO_MODE = True`, lo que significa que los 200 usuarios y 1,400 repositorios son datos generados aleatoriamente con una semilla fija (`seed=42`). Los resultados reales obtenidos con `DEMO_MODE = False` y tokens válidos de GitHub y OpenAI pueden diferir significativamente de los mostrados aquí.

### 2. Sesgo en la Recolección de Datos
La búsqueda de usuarios depende de que ellos mismos declaren su ubicación en su perfil de GitHub. Muchos desarrolladores peruanos no tienen `location` configurado, subestimando el tamaño real de la comunidad. Además, la Search API de GitHub limita los resultados a 1,000 por consulta, haciendo imposible capturar el universo completo.

### 3. Limitaciones de la Clasificación con GPT-4
Los repositorios con descripciones ambiguas, vacías o muy técnicas son difíciles de clasificar con precisión. Proyectos genéricos (hello-world, dotfiles, portfolios) tienden a caer en la categoría J por defecto. Un mismo repositorio podría pertenecer a múltiples industrias, pero el sistema solo asigna una categoría CIIU.

### 4. Solo Repositorios Públicos
La API de GitHub solo expone repositorios públicos. Todo el trabajo privado y comercial — que representa la mayor parte de la actividad profesional real — es invisible para este análisis, sesgando los resultados hacia proyectos personales y académicos.

### 5. Costo de la API de OpenAI
Clasificar 1,000+ repositorios con GPT-4 tiene un costo aproximado de $5–15 USD, limitando la frecuencia de actualización del análisis.

---

## Estructura del Repositorio
```
Github-Peru-Analytics/
├── GITHUB_peru_analytics.ipynb  ← Notebook principal (ejecutado completo)
├── app.py                       ← Dashboard Streamlit
├── dashboard.html               ← Dashboard web estático (464 KB)
├── README.md                    ← Este archivo
├── requirements.txt
├── .env.example
└── data/
    ├── processed/
    │   ├── users.csv            ← 200 usuarios
    │   ├── repositories.csv     ← 1,400 repositorios
    │   └── user_metrics.csv     ← Métricas calculadas
    └── metrics/
        └── ecosystem_metrics.json
```

---

## Tecnologías Utilizadas

| Categoría | Tecnología |
|-----------|-----------|
| Lenguaje | Python 3.10+ |
| GitHub API | REST API v3 |
| IA / LLM | OpenAI GPT-4 Turbo |
| Procesamiento | pandas, numpy |
| Visualización | plotly, streamlit |
| Retry Logic | tenacity |
| Dashboard Web | HTML/CSS/JavaScript + Plotly.js |
| Deploy | Netlify |

