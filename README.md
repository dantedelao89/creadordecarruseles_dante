# Creador de Carruseles — IA CON DANTE

Sistema para generar carruseles de Instagram/TikTok/Facebook con identidad visual propia
(estilo doodle "IA CON DANTE") usando **GPT Image 2 Edit** vía **Wavespeed.ai**, y publicarlos
con el MCP de **Metricool**.

## Estructura

- `referencias/` — anchors visuales (layouts de portada, contenido y CTA).
- `fotos_creador/` — foto del creador para integrar en portadas.
- `output/{tema}_{fecha}/` — carruseles generados (imágenes + copy + caption + prompts + meta).

## Configuración

1. Copia `.env.example` a `.env` y rellena tu `WAVESPEED_API_KEY`.
2. Las imágenes se generan a 4:5 (1080×1424) con paleta: fondo `#ffffff`, texto `#000000`,
   resaltador `#f8f32b`, indigo `#2b2d42`, gris `#8d99ae`.

## Publicación (Metricool)

- Un post por red (captions distintos por plataforma).
- **TikTok** requiere imágenes **JPEG** (no PNG) + título + música.
- **Instagram / Facebook** aceptan PNG.

> ⚠️ El archivo `.env` con la API key NO se versiona (está en `.gitignore`).
