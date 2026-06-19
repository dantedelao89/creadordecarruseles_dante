# 🎨 Creador de Carruseles — IA CON DANTE

Un sistema para crear **carruseles de Instagram, TikTok y Facebook** que siempre se ven
igual de profesionales, sin tener que diseñar cada slide a mano.

La idea es simple: tú escribes el **texto** de cada slide, y el sistema genera las
**imágenes** copiando el estilo de unas plantillas de referencia. Así todos tus carruseles
mantienen la misma identidad visual aunque cambien de tema.

---

## 🧠 ¿Cómo funciona? (explicado fácil)

Imagina que tienes un diseñador que ya sabe exactamente cómo se ve tu marca. Tú le pasas
el texto y él te devuelve las imágenes listas. Eso es esto, pero automático:

```
1. TÚ escribes el copy        →   "Slide 1: Deja de explicarle lo mismo a Claude..."
2. El sistema mira tus         →   carpeta /referencias  (el estilo a copiar)
   plantillas de referencia
3. Genera cada imagen con IA   →   modelo GPT Image 2 Edit (vía Wavespeed.ai)
4. Te las entrega ordenadas    →   carpeta /output/{tema}_{fecha}/
5. (Opcional) las publica       →   en IG, TikTok y Facebook con Metricool
```

**La clave está en las referencias.** El modelo de IA no inventa el diseño desde cero:
toma una de tus plantillas (`referencias/`) y solo **cambia el texto**, respetando los
colores, la tipografía, los íconos dibujados a mano y la composición. Por eso todo sale
coherente.

Para la **portada**, además puede integrar tu **foto** (la de `fotos_creador/`) recortada
de forma profesional.

---

## 📁 Qué hay en cada carpeta

| Carpeta / archivo | Para qué sirve |
|---|---|
| `referencias/` | Las **plantillas de estilo**. Una imagen por tipo de slide (portada, contenido, CTA). El sistema las copia. |
| `fotos_creador/` | Aquí **subes tu propia foto** si quieres aparecer en la portada (tu imagen NO se sube a GitHub). |
| `output/{tema}_{fecha}/` | Aquí aparecen los **carruseles terminados**: imágenes + textos + datos. |
| `.env` | Tu **clave secreta** de Wavespeed (NO se sube a GitHub). |
| `.env.example` | Plantilla para saber qué clave necesitas. |

Dentro de cada carrusel en `output/` encontrarás:
- `slide_01_portada.png`, `slide_02_contenido.png`, … → las **imágenes** numeradas en orden.
- `copy.md` → el texto exacto de cada slide.
- `caption.md` / `captions_multiplataforma.md` → el pie de foto para publicar.
- `prompts.md` → las instrucciones que se usaron para generar cada imagen.
- `meta.json` → ficha técnica (tema, fecha, colores, etc.).

---

## ⚙️ Puesta en marcha (1 sola vez)

1. **Clona el proyecto** (o descárgalo).
2. **Consigue tu clave de Wavespeed** en [wavespeed.ai](https://wavespeed.ai).
3. **Crea tu archivo `.env`**: copia `.env.example`, renómbralo a `.env` y pega tu clave:
   ```bash
   cp .env.example .env
   # luego abre .env y rellena:
   # WAVESPEED_API_KEY=tu_clave_aqui
   ```
4. ¡Listo! Ya puedes pedirle a Claude Code que te genere un carrusel.

> 🔒 **Tu clave nunca se sube a GitHub.** El archivo `.env` está bloqueado en `.gitignore`.

---

## 🎨 Cómo personalizarlo para TU marca

Este sistema está armado con la identidad **"IA CON DANTE"**, pero puedes adaptarlo a
cualquier marca cambiando 4 cosas:

### 1. Las plantillas de estilo (lo más importante)
Reemplaza las imágenes de `referencias/` por las **tuyas**. El sistema copiará ESE estilo.
Conviene tener una referencia por tipo de slide:
- 1 **portada**
- varias de **contenido** (lista, comparación, dato grande, cita…)
- 1 de **CTA** (llamado a la acción)

Mientras más limpias y consistentes sean tus referencias, mejor saldrán los resultados.

### 2. Tu foto
Si quieres **aparecer en la portada**, sube **tu propia foto** a la carpeta `fotos_creador/`
(idealmente de medio cuerpo y con fondo que se pueda recortar fácil). Se usa solo en la
portada y **es opcional**: si no pones ninguna, los carruseles se generan igual, sin persona.

> 🔒 Tu foto **no se sube a GitHub** (está protegida en `.gitignore`), queda solo en tu equipo.

### 3. Los colores y el logo
La identidad actual usa esta paleta. Para cambiarla, solo dile a Claude los colores nuevos
(en código HEX) y el nombre de tu marca:

| Elemento | Color actual |
|---|---|
| Fondo | Blanco `#ffffff` |
| Texto | Negro `#000000` |
| Resaltador / palabras clave | Amarillo `#f8f32b` |
| Cajas, números, ilustraciones | Indigo `#2b2d42` |
| Detalles secundarios | Gris `#8d99ae` |
| Logo inferior | `IA CON DANTE` |

### 4. El formato
Las imágenes salen en **4:5 vertical** (1080×1424), el formato ideal para carruseles de IG.
Si necesitas otro, se cambia en la configuración de generación.

---

## 🤖 ¿Con qué se generan las imágenes?

Con el modelo **GPT Image 2 Edit** a través de la API de **Wavespeed.ai**. La configuración
fija que da buenos resultados es:

```json
{
  "aspect_ratio": "4:5",
  "resolution": "1k",
  "quality": "medium",
  "output_format": "png",
  "enable_sync_mode": true
}
```

El modelo recibe: (1) tu **plantilla de referencia** y (2) **instrucciones** de qué texto
poner y qué colores usar. Devuelve la imagen final ya diseñada.

---

## 📲 Publicar en redes (opcional)

Los carruseles se pueden publicar automáticamente con el **MCP de Metricool**.
Cosas a tener en cuenta por red:

- **Instagram / Facebook** → aceptan imágenes **PNG**. Carrusel de hasta 10 imágenes.
- **TikTok** → solo acepta **JPEG o WEBP** (no PNG), y necesita **título + música**.
- Cada red lleva su **propio pie de foto** (caption), así que se publica un post por red.

---

## ❓ Preguntas rápidas

**¿Necesito saber diseñar?** No. Solo escribes el texto; el diseño lo copia de tus referencias.

**¿Necesito saber programar?** No para usarlo con Claude Code. Le pides el carrusel en
lenguaje normal y él hace el resto.

**¿Cuánto cuesta?** Pagas el uso de la API de Wavespeed por cada imagen generada
(suele ser muy barato). Metricool tiene su propio plan.

**¿Puedo regenerar una sola slide si no me gustó?** Sí, sin rehacer todo el carrusel.

---

> Hecho para crear contenido rápido, consistente y con identidad propia. ✨
