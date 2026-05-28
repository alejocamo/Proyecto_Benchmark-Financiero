# 📊 Financial Analysis · Top 10,000 Companies in Colombia
### Rentabilidad · Riesgo · Eficiencia · Crecimiento — Corte Diciembre 2024

<br>

> **"El ingreso operacional mide el tamaño de una empresa. Los KPIs financieros miden su salud."**  
> Este proyecto demuestra por qué los rankings por ingresos cuentan solo una parte de la historia.

<br>

---

## 🎯 Objetivo

Ir más allá del tamaño medido por ingresos operacionales: identificar qué empresas y sectores de la economía colombiana combinan **mayor rentabilidad con menor riesgo financiero**, utilizando datos oficiales reales publicados por la Superintendencia de Sociedades.

El análisis responde cuatro preguntas concretas de negocio:

1. ¿Qué macrosectores generan mayor rentabilidad (ROE, Margen Neto)?
2. ¿Qué sectores presentan mayor riesgo financiero por endeudamiento?
3. ¿Qué empresas crecieron entre 2023 y 2024 sin sacrificar eficiencia?
4. ¿Cómo se distribuye la salud financiera según tamaño, región y grupo NIIF?

---

## 🔍 Hallazgos Principales

| # | Hallazgo | Valor |
|---|----------|-------|
| H1 | Las empresas pequeñas superan en eficiencia de margen a las grandes | Pequeñas: **3.7%** vs Muy Grandes: **2.7%** margen neto mediano |
| H2 | Las grandes compensan con apalancamiento — ROE cayó en 2024 | ROE mediano: **13.27%** (2023) → **11.97%** (2024) |
| H3 | Minero-Hidrocarburos: mayor margen, menor riesgo, menor ROE | Margen **6.4%** · Endeudamiento **0.6×** · ROE **≈9.9%** |
| H4 | Servicios: mayor ROE del universo, pero mayor apalancamiento | ROE **≈13.3%** · Endeudamiento **≈1.04×** |
| H5 | 2024 fue un año de ajuste defensivo, no de deterioro estructural | Rentabilidad ↓ · Solvencia ↑ · Endeudamiento ↓ |

---

## 🗂️ Estructura del Proyecto

```
analisis-financiero-colombia-2024/
│
├── 📁 datos/
│   ├── Base_1000_empresas_2024.xlsx     ← Top 1.000 por ingresos (Supersociedades)
│   └── Base_9000_empresas_2024.csv      ← Siguientes 9.000 empresas (Supersociedades)
│
├── 📁 notebooks/
│   └── Analisis_Financiero.ipynb        ← Análisis completo: limpieza → KPIs → EDA
│
├── 📁 outputs/
│   ├── 10000_Empresas_Final.csv         ← Dataset enriquecido con KPIs (listo para Power BI)
│   ├── 01_composicion_empresas_por_segmento.png
│   ├── 02_MARGEN_NETO_por_segmento.png
│   ├── 03_ROA_boxplot_segmentos.png
│   ├── 04_ROE_boxplot_segmentos.png
│   ├── 05_ENDEUDAMIENTO_distribucion_segmentos.png
│   ├── 06_TOP_20_ROE.png
│   ├── 07_empresas_crecimiento_eficiente.png
│   └── 08_mapa_rentabilidad_riesgo.png
│
├── requirements.txt
└── README.md
```

---

## 📐 Metodología

### Fuente de datos
Los datos provienen de los informes anuales de la **Superintendencia de Sociedades de Colombia**, disponibles públicamente en:

> 🔗 [supersociedades.gov.co → Sector Real de la Economía](https://www.supersociedades.gov.co/web/asuntos-economicos-societarios/sector-real-de-la-economia)  
> Ruta: Asuntos Económicos Societarios → Dirección de Información Empresarial → Grupo de Estudios Empresariales → Sector Real de la Economía

Se utilizaron los **dos informes más recientes (corte 31 de diciembre de 2024)**:
- Informe de las **1.000 empresas más grandes** de Colombia
- Informe de las **siguientes 9.000 empresas** por ingresos operacionales

Ambos archivos se unificaron en un único dataset de **10.000 registros**.

### Decisiones metodológicas clave

**¿Por qué mediana y no media?**  
El dataset presenta diferencias de magnitud extremas: Ecopetrol factura más de $113 billones, mientras el extremo inferior ronda los $268 millones. La media aritmética se distorsiona severamente ante esta asimetría. La **mediana** representa la empresa "típica" del universo y es el estadístico correcto para análisis comparativos de este tipo.

**¿Por qué conservar los nulos?**  
La proporción de valores nulos en las variables financieras es inferior al 0.5%. Imputarlos o eliminarlos habría alterado rankings y estadísticas sectoriales sin aportar valor analítico real.

**¿Por qué filtros percentílicos en las visualizaciones?**  
Outliers extremos (empresas con ROE de varios miles de por ciento por patrimonio casi en cero) existen y son válidos en el dataset base, pero distorsionan las visualizaciones de distribución. Para las gráficas se aplicaron filtros entre percentiles 5 y 95, dejando los valores originales intactos en el CSV de salida.

### KPIs construidos

Todos los indicadores se calcularon para **2023 y 2024**, permitiendo análisis comparativo anual:

| KPI | Fórmula | Qué mide |
|-----|---------|----------|
| **Margen Neto** | Ganancia / Ingresos × 100 | Eficiencia: cuánto queda de cada peso vendido |
| **ROA** | Ganancia / Activos × 100 | Productividad de los activos |
| **ROE** | Ganancia / Patrimonio × 100 | Rentabilidad para el accionista |
| **Solvencia** | Activos / Pasivos | Capacidad de cubrir todas las deudas |
| **Endeudamiento** | Pasivos / Patrimonio | Nivel de apalancamiento financiero |
| **Crecimiento %** | (Ingresos 2024 − 2023) / 2023 × 100 | Variación real de ingresos año a año |

---

## 📈 Visualizaciones del EDA

El análisis exploratorio cubre **8 visualizaciones** con segmentación simultánea por macrosector, grupo NIIF, departamento y tamaño relativo:

| Gráfica | Tipo | Pregunta que responde |
|---------|------|-----------------------|
| 01 · Composición empresarial | Barras horizontales | ¿Cómo se distribuye el universo? |
| 02 · Margen Neto por segmento | Barras comparativas | ¿Quién es más eficiente operativamente? |
| 03 · ROA por segmento | Boxplot | ¿Quién aprovecha mejor sus activos? |
| 04 · ROE por segmento | Boxplot | ¿Quién genera más valor al accionista? |
| 05 · Endeudamiento | Histograma + KDE | ¿Quién opera con mayor riesgo financiero? |
| 06 · Top 20 por ROE | Ranking horizontal | ¿Cuáles son las empresas más rentables? |
| 07 · Crecimiento eficiente | Scatter | ¿Quién creció sin sacrificar eficiencia? |
| 08 · Mapa estratégico | Bubble chart | ¿Rentabilidad vs riesgo por sector? |

### Visualización central del proyecto

![Mapa Estratégico](outputs/08_mapa_rentabilidad_riesgo.png)

*El mapa integra ROE (rentabilidad) vs Endeudamiento (riesgo) por macrosector. El tamaño de cada burbuja representa el total de ingresos operacionales del sector.*

---

## ⚙️ Cómo reproducir este análisis

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
Los archivos de datos **no están incluidos en el repositorio** por su tamaño. Descárgalos directamente desde Supersociedades:

> 🔗 [Descargar bases de datos](https://www.supersociedades.gov.co/web/asuntos-economicos-sovietarios/sector-real-de-la-economia)

Guarda los archivos en la carpeta `datos/` con los nombres:
- `Base_1000_empresas_2024.xlsx`
- `Base_9000_empresas_2024.csv`

### 4. Ejecutar el notebook
```bash
jupyter notebook notebooks/Analisis_Financiero.ipynb
```

Ejecuta todas las celdas en orden. El notebook genera automáticamente las 8 gráficas y el CSV de salida en la carpeta `outputs/`.

---

## 🛠️ Stack Tecnológico

| Herramienta | Uso |
|-------------|-----|
| **Python 3.12** | Lenguaje base |
| **pandas** | Manipulación y transformación de datos |
| **numpy** | Cálculos numéricos y KPIs financieros |
| **matplotlib** | Visualizaciones base |
| **seaborn** | Visualizaciones estadísticas (boxplots, KDE) |
| **Power BI** | Dashboard interactivo *(próxima fase)* |

---

## 📋 Limitaciones del análisis

- Los datos de Supersociedades **no cubren el universo completo** de empresas colombianas: excluye microempresas informales, entidades financieras supervisadas por la Superfinanciera, y empresas con ingresos por debajo del umbral de reporte.
- Los KPIs calculados son **indicadores contables**, no de mercado. No reflejan valoraciones de mercado ni flujos de caja.
- El análisis es **descriptivo y exploratorio** — las correlaciones observadas entre variables no implican causalidad.
- La clasificación por "tamaño relativo" se basa en **cuartiles del dataset**, no en la definición oficial del Ministerio de Comercio de Colombia.

---

## 🚀 Próximas fases del proyecto

- [ ] **Dashboard interactivo en Power BI** — 3 paneles: composición, KPIs por sector, ranking de empresas
- [ ] **Modelo de clasificación de riesgo** — identificar empresas con perfil de riesgo elevado usando ML
- [ ] **Análisis de series de tiempo** — incorporar datos 2021–2024 para tendencias de largo plazo

---

## 👤 Autor

**Alejandro Castro Montoya**  
Data Analyst · Finanzas & Estrategia de Negocio

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?logo=linkedin)](https://linkedin.com/in/tu-perfil)
[![GitHub](https://img.shields.io/badge/GitHub-Portfolio-black?logo=github)](https://github.com/tu-usuario)

---

## 📄 Fuente de Datos — Citación

> Superintendencia de Sociedades de Colombia. (2025).  
> *Informe de las 1.000 empresas más grandes de Colombia — Cierre 2024.*  
> Dirección de Información Empresarial y Estudios Económicos y Contables.  
> Recuperado de: https://www.supersociedades.gov.co/web/asuntos-economicos-societarios/sector-real-de-la-economia

---

*Proyecto desarrollado como parte de un proceso de formación en Data Science aplicado a Finanzas y Estrategia de Negocio.*
