# AGENTS.md — Guía para agentes de código

> Este archivo está escrito en español porque todo el proyecto, la documentación, los comentarios y los activos se mantienen en ese idioma.

## 1. Visión general del proyecto

Este repositorio aloja la **página web de divulgación y los documentos académicos** del proyecto de investigación **“Método de Optimización en modelos CNN mediante técnica de reducción de modelos para la clasificación de imágenes médicas en dispositivos de recursos limitados”**, presentado para la **Jornada Científica 2026** de la **Universidad Peruana Unión (UPeU)**, Facultad de Ingeniería y Arquitectura, Escuela Profesional de Ingeniería de Sistemas.

**Equipo de investigación:**

- Alexis Del Castillo Yunca (0009-0003-7326-7873)
- Luis Keny Lucero Balvin (0009-0006-8952-1719)
- May Attilano Cango (0009-0007-9881-2638)
- Asesor: Ferdinand Pineda Ancco
- Co-asesor: Nemias Saboya Rios

**Objetivo general:** desarrollar un método de optimización de modelos de visión computacional aplicados a imágenes médicas que reduzca el costo computacional sin comprometer significativamente las métricas de rendimiento diagnóstico, habilitando su despliegue en dispositivos con recursos restringidos.

El repositorio **no contiene el código de entrenamiento ni los pesos de los modelos**. Es un repositorio de presentación que incluye:

- `index.html`: sitio web estático de divulgación con la propuesta, objetivos, metodología, resultados y conclusiones.
- `PPI/PPI 2026 - metodo de optimizacion.docx`: perfil de proyecto de investigación (documento académico principal).
- `PPT Plantilla/Plantilla Jornada Científica (2).pptx`: plantilla de presentación para la jornada.
- `Metodologia/FASE 1.png` … `FASE 5.png`: diagramas del pipeline de 5 fases.
- `Resultados/reporte_tesis.xlsx`: libro de Excel con las métricas finales, comparaciones y configuraciones YAML de los experimentos.
- `CLAUDE.md`: guía rápida para Claude Code con el contexto del proyecto.

## 2. Stack tecnológico y arquitectura

### 2.1 Sitio web (`index.html`)

- **HTML5 semántico** en un único archivo (`index.html`).
- **CSS embebido** en la sección `<style>`; no usa frameworks CSS externos.
- **JavaScript embebido** al final del cuerpo; únicamente para inicializar dos gráficos con **Chart.js 4.4.0** cargado desde CDN (`https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js`).
- **No hay backend ni build**: se abre directamente en un navegador.
- Paleta de colores institucional de UPeU: azul `#003865`, dorado `#F5A800`, fondo claro `#E8F0F8`.
- Diseño responsive manual con media queries.

### 2.2 Pipeline experimental (documentado, no presente como código fuente)

Los documentos (`docx`, `xlsx`) describen un pipeline de 4-5 fases ejecutado con Python/PyTorch. Aunque los scripts no están en este repositorio, el AGENT debe conocerlo para no contradecir la documentación:

| Fase | Nombre | Tecnología / salida clave |
|------|--------|---------------------------|
| 1 | Entrenamiento base | PyTorch / `timm` (EfficientNetV2-S, MobileNetV4) o Ultralytics YOLO (YOLO26n/s/m/l/x); optimizador AdamW; salida `best.pt` / `modelo_entrenado.pt`. |
| 2 | Pruning | Método Taylor o magnitud; ratio 0.3; salida `pruned.pt` / `modelo_podado.pt`. |
| 3 | Fine-tuning | Knowledge Distillation (α=0.5, T=4.0) o scheduler; salida `finetuned.pt`. |
| 4 | Cuantización | PTQ INT8 vía ONNX (`opset_version=17`, 10 batches de calibración); salida `modelo_int8.onnx`. |
| 5 | Evaluación | MLflow: comparación de métricas diagnósticas y computacionales. |

**Datasets utilizados** (según las configuraciones del Excel):

- `ojo_dr_binary_v1.0` — retinopatía diabética.
- `oral_cancer_binary_v1.0` / `oral_cancer_v2_binary_v1.0` — cáncer oral.
- `skin_melanoma` — melanoma de piel.
- `unas_melanoma` — uñas (posible extensión).

**Métricas reportadas:** Accuracy, Recall, Specificity, F1-score, AUC-ROC, tamaño del modelo (MB), latencia de inferencia (ms), speedup.

## 3. Estructura del repositorio

```text
Investigacion-2027/
├── AGENTS.md          # Este archivo
├── CLAUDE.md          # Guía para Claude Code
├── index.html         # Página web estática de divulgación
├── Metodologia/       # Diagramas PNG del pipeline de 5 fases
│   ├── FASE 1.png
│   ├── FASE 2.png
│   ├── FASE 3.png
│   ├── FASE 4.png
│   └── FASE 5.png
├── PPI/               # Documento académico principal (Word)
│   └── PPI 2026 - metodo de optimizacion.docx
├── PPT Plantilla/     # Plantilla de presentación (PowerPoint)
│   └── Plantilla Jornada Científica (2).pptx
└── Resultados/        # Resultados experimentales (Excel)
    └── reporte_tesis.xlsx
```

## 4. Cómo ejecutar / visualizar

### Sitio web

No requiere instalación ni servidor. Opciones:

```bash
# Abrir con el navegador por defecto (Windows/Git Bash)
start index.html

# O simplemente abrir el archivo directamente
cat index.html
```

Para previsualizar cambios de forma local se puede levantar un servidor estático liviano:

```bash
# Python 3
python -m http.server 8000
# Luego abrir http://localhost:8000
```

### Documentos Word / PowerPoint / Excel

Son archivos binarios de Microsoft Office (formato OOXML). Se editan con Microsoft Word, PowerPoint y Excel respectivamente. Para extraer texto o inspeccionarlos desde la terminal:

```bash
# Extraer texto del documento Word
unzip -p "PPI/PPI 2026 - metodo de optimizacion.docx" word/document.xml | sed 's/<[^>]*>//g' | tr -s ' \n'

# Listar hojas del Excel
unzip -p Resultados/reporte_tesis.xlsx xl/workbook.xml

# Extraer cadenas compartidas del Excel
unzip -p Resultados/reporte_tesis.xlsx xl/sharedStrings.xml | sed 's/<[^>]*>//g' | tr -s ' \n'
```

## 5. Convenciones de estilo y edición

### `index.html`

- **Un único archivo**: todo el CSS, HTML y JS vive en `index.html`. Evita crear archivos adicionales salvo que sea estrictamente necesario.
- **Idioma español**: todos los textos de la interfaz, comentarios y `alt` deben estar en español.
- **CSS custom properties**: usa las variables definidas en `:root` (`--upeu-blue`, `--upeu-gold`, etc.). No introduzcas colores hardcodeados arbitrarios.
- **Comentarios seccionadores**: usa el patrón existente:
  ```html
  <!-- ══════════════════════════════════════
       N. NOMBRE DE SECCIÓN
  ══════════════════════════════════════ -->
  ```
- **Datos de resultados**: los gráficos de Chart.js consumen arreglos de datos embebidos en JavaScript. Si actualizas resultados, mantén la correspondencia entre la tabla HTML (`#resultados`) y los arreglos de `sizeChart` / `aucChart`.
- **Accesibilidad básica**: mantén `lang="es"`, contrastes de color y estructura semántica (`section`, `nav`, `footer`).

### Documentos Office

- No modifiques los archivos `.docx`, `.pptx` ni `.xlsx` a menos de que el usuario lo solicite explícitamente, dado que son entregables académicos.
- Si debes actualizarlos, usa las aplicaciones oficiales de Microsoft o librerías Python como `python-docx` / `openpyxl` para no corromper el OOXML.

## 6. Pruebas

Este repositorio **no tiene suite de pruebas automatizadas**. Las validaciones manuales recomendadas al editar `index.html` son:

1. Abrir el archivo en Chrome / Edge / Firefox y verificar que no haya errores en la consola del desarrollador (F12).
2. Comprobar que los gráficos de Chart.js se renderizan correctamente.
3. Revisar la vista responsive con el modo de dispositivos del navegador (ancho < 700 px).
4. Validar que todos los enlaces internos del menú de navegación (`#portada`, `#problematica`, etc.) funcionen.

## 7. Consideraciones de seguridad

- **No hay secretos ni credenciales** en el repositorio actual.
- `index.html` carga Chart.js desde CDN (`cdn.jsdelivr.net`). Si se requiere uso offline, descarga la librería y referénciala localmente.
- Los documentos Word/Excel pueden contener metadatos de autor. No los publiques públicamente si contienen información sensible o sin revisar.
- El repositorio está vinculado a un remoto de GitHub (`MrDac070200/Investigacion-2027`). No realices `git push` sin confirmación explícita del usuario.

## 8. Notas para el agente

- El proyecto es **documental / de divulgación**, no un codebase de ML ejecutable. Si el usuario pide “entrenar”, “probar el modelo” o “correr el pipeline”, indica amablemente que este repositorio no contiene los scripts ni los datos; solo la página web y los entregables académicos.
- Cualquier modificación en `index.html` debe respetar la identidad visual de UPeU y la estructura de secciones ya establecida.
- Si se añaden nuevos resultados, sincroniza: tabla HTML, KPIs, gráficos de Chart.js y, si aplica, la hoja `Resultados/reporte_tesis.xlsx`.
