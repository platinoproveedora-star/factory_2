# vertical_instagram

Automatiza la gestión completa de una cuenta de Instagram específica.
Un agente maestro orquesta sub-agentes que planifican, generan y publican contenido.

## Objetivo

Construir la vertical completa para que cualquier fábrica pueda conectar una cuenta de Instagram y operarla de forma autónoma: calendario editorial, generación de contenido, publicación, analytics y comunidad.

## Estado

Inicio — vertical definida, skills y agentes mapeados, pendiente de construcción.

## Skills planeados

### Contenido
- `ig_caption_generator` — caption + CTA con tono de marca
- `ig_hashtag_generator` — hashtags por nicho y alcance
- `ig_carousel_builder` — estructura slides de carrusel con copy
- `ig_story_script` — guión para historia con stickers y CTA
- `ig_reel_script` — guión corto para Reel con hook inicial
- `ig_content_brief` — brief de contenido por objetivo de campaña

### Publicación
- `ig_post_image` — sube imagen + caption vía Graph API
- `ig_post_carousel` — sube carrusel multi-imagen
- `ig_schedule_post` — programa publicación con fecha/hora
- `ig_get_analytics` — lee métricas de posts (alcance, engagement)
- `ig_reply_comment` — responde comentarios automáticamente

### Planificación
- `ig_calendar_generator` — genera calendario editorial mensual

## Agentes planeados

- `ig_content_agent` — genera todo el contenido de un post (caption, hashtags, imagen brief)
- `ig_publisher_agent` — ejecuta la publicación en el momento correcto
- `ig_analytics_agent` — lee métricas y sugiere ajustes
- `ig_community_agent` — responde comentarios y DMs con tono de marca
- `ig_master_agent` — orquesta todos los anteriores, maneja el calendario completo

## Decisiones de diseño

- Skills de publicación (los que tocan Meta Graph API) se mantienen delgados para facilitar actualizaciones cuando Meta cambie endpoints.
- Lógica de contenido (captions, hashtags, calendarios) es independiente de Meta.
- El agente maestro orquesta sin acoplarse a los skills de publicación directamente.

## Variables de entorno requeridas

```
IG_ACCESS_TOKEN=
IG_BUSINESS_ACCOUNT_ID=
ANTHROPIC_API_KEY=
```

## Próximo paso

Construir el primer skill: `ig_caption_generator`.
