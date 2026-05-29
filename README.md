# 📊 Análisis Financiero · Top 10.000 Empresas más Grandes de Colombia
### Rentabilidad · Riesgo · Eficiencia · Crecimiento — Corte Diciembre 2024

<br>

> **"El ingreso operacional mide el tamaño de una empresa. Los KPIs financieros miden su salud."**  
> Este proyecto demuestra por qué los rankings por ingresos cuentan solo una parte de la historia.

<br>

![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-F2C811?logo=powerbi&logoColor=black)
![Supersociedades](https://img.shields.io/badge/Fuente-Supersociedades%20Colombia-003087)
![Status](https://img.shields.io/badge/Estado-Completo-065F46)

---

## 🎯 Objetivo

¿Qué significa realmente que una empresa sea **"grande"** en Colombia?

Este proyecto nació de una convicción: el ingreso operacional mide tamaño, no salud financiera. Una empresa puede facturar billones y estar destruyendo valor para sus accionistas. Puede crecer en ventas y simultáneamente contraer márgenes.

El análisis va más allá del ranking por ingresos e identifica qué empresas y sectores combinan **mayor rentabilidad con menor riesgo financiero**, utilizando datos oficiales reales de la Superintendencia de Sociedades.

**Cuatro hipótesis guían el análisis:**

| # | Hipótesis |
|---|-----------|
| H1 | Las empresas con mayores ingresos no necesariamente son las más rentables |
| H2 | El tamaño por ingresos no implica eficiencia operativa |
| H3 | Algunos sectores requieren grandes activos para generar márgenes mínimos |
| H4 | Empresas medianas pueden superar a grandes corporaciones en retorno sobre activos |

---

## 📁 Dataset

Los datos provienen de la **Superintendencia de Sociedades de Colombia**, fuente oficial del Estado:

> 🔗 [supersociedades.gov.co → Sector Real de la Economía](https://www.supersociedades.gov.co/web/asuntos-economicos-societarios/sector-real-de-la-economia)  
> Ruta: *Asuntos Económicos Societarios → Dirección de Información Empresarial → Grupo de Estudios Empresariales → Sector Real de la Economía*

Se utilizaron los dos informes con **corte al 31 de diciembre de 2024**, unificados en un único dataset:

| Archivo | Descripción | Registros |
|---------|-------------|-----------|
| `Base_1000_empresas_2024.xlsx` | Top 1.000 empresas por ingresos | 1.000 |
| `Base_9000_empresas_2024.csv` | Siguientes 9.000 empresas | 9.000 |
| `outputs/10000_Empresas_Final.csv` | Dataset unificado con KPIs calculados | **10.000** |

> ⚠️ Los archivos fuente **no están incluidos en el repositorio** por su tamaño. Descárgalos directamente desde el enlace de Supersociedades y ubícalos en la carpeta `datos/`.

**Decisiones metodológicas clave:**

- **¿Por qué mediana y no media?** Ecopetrol factura $113 billones; el extremo inferior ronda $268 millones. La media queda distorsionada por los gigantes del tope. La mediana representa la empresa "típica" y es el estadístico correcto para esta comparación.
- **¿Por qué conservar los nulos?** La proporción de nulos en variables financieras es inferior al 0.5% — imputarlos alteraría rankings y estadísticas sectoriales sin aportar valor real.
- **¿Por qué filtros percentílicos en el ranking?** Para el ROE se aplicó un rango percentil 5-95 y se filtraron únicamente empresas con patrimonio positivo, garantizando interpretación económica válida.

---


**Entorno:** `venv` con dependencias reproducibles en `requirements.txt`

```
analisis-financiero-colombia-2024/
│
├── 📁 datos/
│   ├── Base_1000_empresas_2024.xlsx        ← Top 1.000 por ingresos (Supersociedades)
│   └── Base_9000_empresas_2024.csv         ← Siguientes 9.000 empresas (Supersociedades)
│
├── 📁 notebooks/
│   └── Analisis_Financiero.ipynb           ← Análisis completo: limpieza → KPIs → EDA
│
├── 📁 outputs/
│   ├── 10000_Empresas_Final.csv            ← Dataset enriquecido con KPIs (fuente Power BI)
│   ├── 01_composicion_empresas_por_segmento.png
│   ├── 02_MARGEN_NETO_por_segmento.png
│   ├── 03_ROA_boxplot_segmentos.png
│   ├── 04_ROE_boxplot_segmentos.png
│   ├── 05_ENDEUDAMIENTO_distribucion_segmentos.png
│   ├── 06_TOP_20_ROE.png
│   ├── 07_empresas_crecimiento_eficiente.png
│   ├── 08_mapa_rentabilidad_riesgo.png
│   └── 📁 Dashboard_PNGs/                  ← Capturas visuales del dashboard Power BI
│       ├── Panel_01_Vista_General.png
│       ├── Panel_02_KPIs_Financieros.png
│       └── Panel_03_Ranking_Empresas.png
│
├── requirements.txt
└── README.md
```

---

## 📊 EDA — Análisis Exploratorio de Datos

Se construyeron **6 KPIs financieros** para cada empresa, calculados para 2023 y 2024:

| KPI | Fórmula | Qué mide |
|-----|---------|----------|
| **Margen Neto** | Ganancia / Ingresos × 100 | Cuánto queda de cada peso vendido |
| **ROA** | Ganancia / Activos × 100 | Productividad de los activos |
| **ROE** | Ganancia / Patrimonio × 100 | Rentabilidad para el accionista |
| **Solvencia** | Activos / Pasivos | Capacidad de cubrir todas las deudas |
| **Endeudamiento** | Pasivos / Patrimonio | Nivel de apalancamiento financiero |
| **Crecimiento %** | (Ingresos 2024 − 2023) / 2023 × 100 | Variación real de ingresos año a año |

El análisis exploratorio cubre **8 visualizaciones** con segmentación simultánea por macrosector, grupo NIIF, departamento y tamaño relativo:

| # | Gráfica | Tipo | Pregunta que responde |
|---|---------|------|-----------------------|
| 01 | Composición empresarial | Barras horizontales | ¿Cómo se distribuye el universo? |
| 02 | Margen Neto por segmento | Barras comparativas | ¿Quién es más eficiente operativamente? |
| 03 | ROA por segmento | Boxplot | ¿Quién aprovecha mejor sus activos? |
| 04 | ROE por segmento | Boxplot | ¿Quién genera más valor al accionista? |
| 05 | Endeudamiento | Histograma + KDE | ¿Quién opera con mayor riesgo financiero? |
| 06 | Top 20 por ROE | Ranking horizontal | ¿Cuáles son las empresas más rentables? |
| 07 | Crecimiento eficiente | Scatter plot | ¿Quién creció sin sacrificar eficiencia? |
| 08 | Mapa estratégico | Bubble chart | ¿Rentabilidad vs riesgo por sector? |

**Visualización central del proyecto:**

![Mapa Estratégico](outputs/08_mapa_rentabilidad_riesgo.png)

*El mapa integra ROE (rentabilidad) vs Endeudamiento (riesgo) por macrosector. El tamaño de cada burbuja representa el total de ingresos operacionales del sector. Ningún sector domina en todas las dimensiones — la respuesta a "¿cuál es el mejor?" depende del perfil de riesgo del analista.*

---

## 🤖 Modelado y Métricas Clave

### Resumen estadístico del universo · mediana (robusto a outliers)

| KPI | Mediana 2023 | Mediana 2024 | Variación |
|-----|-------------|-------------|-----------|
| Margen Neto | 3.49% | 3.21% | ▼ -0.28 pp |
| ROA | 5.39% | 4.85% | ▼ -0.54 pp |
| ROE | 13.27% | 11.97% | ▼ -1.30 pp |
| Solvencia | 1.79× | 1.83× | ▲ +0.04× |
| Endeudamiento | 1.20× | 1.14× | ▼ -0.06× |

> La caída simultánea de los tres indicadores de rentabilidad con mejora en los dos indicadores de riesgo configura un **ajuste defensivo**: las empresas colombianas sacrificaron rentabilidad de corto plazo para reducir su exposición financiera en un entorno de tasas de interés históricamente altas (2023-2024).

### Resumen por macrosector · 2024

| Macrosector | Empresas | Margen | ROE | Endeudamiento | Perfil |
|-------------|----------|--------|-----|---------------|--------|
| Minero-HC | 182 | **6.4%** | 9.9% | 0.6× | Conservador |
| Construcción | 756 | 4.5% | 11.3% | 1.25× | Balanceado |
| Servicios | 3.332 | 4.2% | **13.3%** | 1.04× | Dinámico |
| Manufactura | 1.920 | 3.9% | 11.4% | 1.08× | Estable |
| Agropecuario | 393 | 3.6% | 9.5% | 0.8× | Conservador |
| Comercio | 3.417 | 2.0% | 11.5% | **1.26×** | Alto volumen |

---

## 📈 Dashboard Power BI

El análisis exploratorio se complementa con un **dashboard interactivo en Power BI** que permite navegar, filtrar y cruzar los datos dinámicamente con filtros por macrosector, grupo NIIF, región y año.

### 🔗 [→ Ver dashboard público interactivo]
https://app.powerbi.com/view?r=eyJrIjoiODA3N2NlNWMtZWE0MC00N2Q0LTljNjItZmQ2Mjg3ODQxYmM4IiwidCI6IjU3N2ZjMWQ4LTA5MjItNDU4ZS04N2JmLWVjNGY0NTVlYjYwMCIsImMiOjR9&pageName=ddc34be5f83514245e50

> Las capturas visuales de los tres paneles están disponibles en [`outputs/Dashboard_PNGs/`](outputs/Dashboard_PNGs/) para previsualización rápida sin abrir Power BI.

---

### Panel 1 · Vista General — Composición y contexto

![Panel 1 Vista General](outputs/Dashboard_PNGs/Panel_01_Vista_General.png)

KPIs maestros del universo (10.000 empresas · 8.571 con utilidad positiva · Margen 3.21% · ROE 11.97%), distribución por macrosector, treemap de peso en ingresos, mapa geográfico por departamentos y tabla resumen con formato condicional.

**Filtros:** Macrosector · Grupo NIIF · Región · Año (2023 / 2024)

---

### Panel 2 · KPIs Financieros — Análisis comparativo

![Panel 2 KPIs](outputs/Dashboard_PNGs/Panel_02_KPIs_Financieros.png)

Selector de KPI activo con visualización dinámica, variación año a año (2023 vs 2024) por sector, **mapa estratégico interactivo ROE vs Endeudamiento** con burbujas por volumen de ingresos, y boxplot de distribución por segmento seleccionado.

**Filtros:** KPI activo · Segmento (Macrosector / Grupo NIIF / Departamento)

---

### Panel 3 · Ranking — Empresas y perfil financiero

![Panel 3 Ranking](outputs/Dashboard_PNGs/Panel_03_Ranking_Empresas.png)

Top N configurable (10 / 20 / 30 / 40 / 50) por cualquier KPI. Al seleccionar una empresa se activa el perfil completo comparado vs la mediana del sector. Solo empresas con patrimonio positivo en percentil 95% para robustez estadística.

> 💡 **Hallazgo visible en el ranking:** Las Top 20 empresas por ROE no son las grandes corporaciones del ranking por ingresos. Son clínicas, distribuidoras especializadas, tech y agroindustria de nicho. La empresa #1 — **Asesorías e Ingenierías Servicios y Suministros SAS** — registra un ROE de **59.87%**.

---

## 🔍 Insights Principales

| # | Hallazgo | Evidencia |
|---|----------|-----------|
| **H1 ✅** | El tamaño no garantiza eficiencia operativa | Empresas "Pequeñas": margen **3.7%** vs "Muy Grandes": **2.7%** |
| **H2 ✅** | Las grandes compensan con apalancamiento — y en 2024 eso costó | ROE cayó **13.27% → 11.97%** (-1.30 pp) |
| **H3 ✅** | Minero-HC: paradoja de escala | Margen líder (**6.4%**) pero ROE más bajo (**9.9%**) por patrimonio enorme |
| **H4 ✅** | Servicios: el sector más dinámico y más apalancado | ROE **13.3%** con endeudamiento **1.04×** — mayor riesgo-retorno |
| **H5** | 2024: ajuste defensivo, no deterioro estructural | Rentabilidad ↓ + Solvencia ↑ + Endeudamiento ↓ simultáneamente |

**Conclusión central:**

> No existe una empresa ni un sector "mejor" en todas las dimensiones. El análisis demuestra que el tamaño en ingresos es solo una dimensión de una historia financiera mucho más compleja — y que los datos, bien tratados, cuentan esa historia con precisión.

---

## ⚙️ Cómo Ejecutar

### 1. Clonar el repositorio
```bash
git clone https://github.com/tu-usuario/analisis-financiero-colombia-2024.git
cd analisis-financiero-colombia-2024
```

### 2. Crear entorno virtual e instalar dependencias
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac / Linux
source venv/bin/activate

pip install -r requirements.txt
```

### 3. Descargar los datos originales
Los archivos fuente **no están incluidos** por su tamaño. Descárgalos desde:

> 🔗 [Superintendencia de Sociedades → Sector Real de la Economía](https://www.supersociedades.gov.co/web/asuntos-economicos-societarios/sector-real-de-la-economia)

Guárdalos en `datos/` con los nombres indicados en la sección Dataset.

### 4. Ejecutar el notebook
```bash
jupyter notebook notebooks/Analisis_Financiero.ipynb
```

Ejecuta todas las celdas en orden. El notebook genera automáticamente las 8 gráficas y el CSV final en `outputs/`.

---

## 📋 Limitaciones

- Los datos de Supersociedades **no cubren el universo completo**: excluye microempresas informales, entidades financieras de la Superfinanciera, y empresas por debajo del umbral de reporte.
- Los KPIs son **indicadores contables**, no de mercado. No reflejan valoraciones ni flujos de caja libres.
- El análisis es **descriptivo y exploratorio** — las correlaciones observadas no implican causalidad.
- La clasificación "tamaño relativo" se basa en cuartiles del dataset, no en la definición oficial del Ministerio de Comercio de Colombia.

---

## 👤 Autor

**Alejandro Castro Montoya**  
Data Analyst · Finanzas & Estrategia de Negocio

![Linkedin] www.linkedin.com/in/alejandro-castro-ingeniero
![Power BI] https://app.powerbi.com/view?r=eyJrIjoiODA3N2NlNWMtZWE0MC00N2Q0LTljNjItZmQ2Mjg3ODQxYmM4IiwidCI6IjU3N2ZjMWQ4LTA5MjItNDU4ZS04N2JmLWVjNGY0NTVlYjYwMCIsImMiOjR9&pageName=ddc34be5f83514245e50

---

*Proyecto desarrollado como parte de un proceso de formación en Data Science aplicado a Finanzas y Estrategia de Negocio · Colombia 2025*
