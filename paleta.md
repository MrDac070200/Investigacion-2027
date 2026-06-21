````markdown
# Guía de Aplicación de la Paleta de Colores

## Objetivo

La identidad visual se basa en una combinación de tonos azules como colores principales, tonos amarillos como colores de énfasis y una base neutra blanca para garantizar claridad, contraste y una apariencia profesional.

---

# Paleta Principal

| Tipo | Color | Hex |
|--------|--------|--------|
| Primario Principal | Azul Marino | `#003865` |
| Primario Oscuro | Azul Marino Oscuro | `#00305F` |
| Secundario Principal | Amarillo Dorado | `#F8A900` |
| Fondo Principal | Blanco Grisáceo | `#F7F7F7` |
| Blanco Puro | Blanco | `#FFFFFF` |

---

# Principios Generales

- Los tonos azules representan la identidad principal de la marca.
- Los tonos amarillos deben utilizarse únicamente para destacar elementos importantes.
- El fondo debe mantenerse claro para favorecer la legibilidad.
- Se debe preservar un contraste adecuado entre texto y fondo.
- Evitar el uso excesivo del amarillo para no competir con la jerarquía visual del azul.

---

# Jerarquía de Uso

## 1. Color Primario (70%)

Los tonos azules constituyen el color dominante de la interfaz.

### Aplicaciones

- Encabezados.
- Barras de navegación.
- Menús laterales.
- Botones principales.
- Títulos de secciones.
- Iconos principales.
- Gráficos y diagramas.
- Elementos destacados de identidad visual.

### Colores permitidos

```css
#003865
#00305F
```

---

## 2. Color Secundario (20%)

El amarillo se utiliza exclusivamente como color de énfasis.

### Aplicaciones

- Botones de acción importantes.
- Indicadores activos.
- Etiquetas y badges.
- Resaltado de información relevante.
- Iconos de atención.
- Elementos interactivos importantes.

### Color permitido

```css
#F8A900
```

### Recomendaciones

✔ Usar para llamar la atención.

✔ Utilizar de forma moderada.

✘ No usar como fondo dominante.

✘ No emplear para bloques extensos de texto.

---

## 3. Fondo (10%)

Los colores blancos proporcionan limpieza visual y mejoran la legibilidad.

### Aplicaciones

- Fondo general de la interfaz.
- Tarjetas.
- Contenedores.
- Formularios.
- Tablas.
- Modales.

### Colores permitidos

```css
#F7F7F7
#FFFFFF
```

---

# Uso del Texto

## Texto sobre fondo claro

```css
Color: #003865
```

### Ejemplo

- Títulos
- Párrafos
- Etiquetas
- Formularios

---

## Texto sobre fondo azul

```css
Color: #FFFFFF
```

### Ejemplo

- Botones primarios
- Encabezados
- Tarjetas con fondo azul

---

## Texto sobre fondo amarillo

```css
Color: #003865
```

### Ejemplo

- Botones secundarios
- Indicadores
- Badges

---

# Botones

## Botón Primario

Fondo:

```css
#003865
```

Texto:

```css
#FFFFFF
```

Hover:

```css
#00305F
```

---

## Botón Secundario

Fondo:

```css
#F8A900
```

Texto:

```css
#003865
```

Hover:

```css
#E39B00
```

---

# Tarjetas y Contenedores

## Fondo

```css
#FFFFFF
```

## Borde

```css
rgba(0,56,101,0.1)
```

## Título

```css
#003865
```

## Contenido

```css
#4A4A4A
```

---

# Alertas

## Información

Fondo:

```css
#EAF3FB
```

Texto:

```css
#003865
```

---

## Advertencia

Fondo:

```css
#FFF5DE
```

Texto:

```css
#003865
```

Icono:

```css
#F8A900
```

---

# Proporción Recomendada

| Tipo de color | Proporción |
|---------------|-----------|
| Azul (Primario) | 70% |
| Blanco (Fondo) | 20% |
| Amarillo (Énfasis) | 10% |

---

# Reglas de Diseño

### ✔ Recomendado

- Mantener predominio de los tonos azules.
- Utilizar el amarillo únicamente para destacar acciones o información importante.
- Conservar fondos claros para maximizar la legibilidad.
- Usar suficiente espacio en blanco.
- Mantener una apariencia moderna y profesional.

### ✘ Evitar

- Utilizar grandes superficies amarillas.
- Mezclar colores adicionales que rompan la identidad visual.
- Emplear texto amarillo sobre fondo blanco.
- Usar azul sobre fondos oscuros.
- Saturar la interfaz con demasiados elementos de color.

---

# Variables CSS

```css
:root {

    /* Colores primarios */
    --color-primary: #003865;
    --color-primary-dark: #00305F;

    /* Colores secundarios */
    --color-secondary: #F8A900;

    /* Fondos */
    --color-background: #F7F7F7;
    --color-surface: #FFFFFF;

    /* Texto */
    --color-text-primary: #003865;
    --color-text-secondary: #4A4A4A;
    --color-text-on-primary: #FFFFFF;

}
```

---

# Identidad Visual

La identidad visual debe transmitir:

- Profesionalismo.
- Tecnología.
- Confianza.
- Modernidad.
- Claridad.
- Simplicidad.
- Accesibilidad.
- Consistencia visual.
````
