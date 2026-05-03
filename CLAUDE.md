# factory2 - Contexto del Proyecto

## Que es

`factory2` es una fabrica generica de bots, agentes y skills portables.

Es un repo independiente generado desde la fabrica madre, pero ya no depende de nombres legacy del proyecto original.

## Estructura real

```txt
factory2/
  factory/
    engine/
    skills/
      internos/
      registry.json
    agents/
      registry.json
    bots/
      registry.json
    mcp/
      registry.json
  factory_api.py
  requirements.txt
  README.md
  .env.example
```

## Runtime

- API: `factory_api.py`
- FastAPI app: `factory_api:app`
- Carpeta base: `factory/`
- Engine: `factory.engine`
- Skills internos: `factory/skills/internos/<skill_name>/`
- Registry de skills: `factory/skills/registry.json`

## Contrato de skill

Cada skill ejecutable debe tener:

```txt
skill.py
service.py
manifest.json
SKILL.md
```

El entrypoint publico es:

```python
def run(context: dict) -> dict:
    ...
```

## Verticales incluidas

- `factory`
- `factory_skills`
- `factory_github`
- `factory_render`
- `factory_telegram`
- `factory_supabase`
- `marketing_ai`
- `utils`
- `security`

## Skills clave

- `new_factory`: genera otra fabrica local o cloud.
- `verify_new_factory`: valida una fabrica generada.
- `new_skill`: crea skills internos.
- `add_skill`: importa skills externos.
- `export_skill_pack`: exporta skills por vertical.
- `verify_skill_pack`: valida packs exportados.
- `new_agent`: crea agentes.
- `add_bot`: crea bots Telegram.
- `add_agent_brain`: agrega brain Anthropic a un agente.
- `connect_bot_agent`: conecta bot con agente.

## Variables de entorno

Usar `.env.example` como base.

Variables comunes:

```txt
ANTHROPIC_API_KEY=
TELEGRAM_TOKEN=
ADMIN_BOT_TOKEN=
ADMIN_CHAT_ID=
GITHUB_TOKEN=
RENDER_API_KEY=
RENDER_OWNER_ID=
SUPABASE_URL=
SUPABASE_PROJECT_REF=
SUPABASE_ACCESS_TOKEN=
SUPABASE_SERVICE_ROLE_KEY=
SUPABASE_ANON_KEY=
```

No usar nombres legacy para variables admin. Usar `ADMIN_BOT_TOKEN` y `ADMIN_CHAT_ID`.

## Pruebas rapidas

Desde la raiz de `factory2`:

```bash
python -m compileall factory factory_api.py
python -c "import factory_api; print(factory_api.root()); print(factory_api.health())"
```

Para correr API local:

```bash
uvicorn factory_api:app --reload
```

Luego abrir:

```txt
http://127.0.0.1:8000/health
```

## Git y deploy

Siguiente flujo recomendado:

1. Inicializar git en `factory2`.
2. Crear primer commit.
3. Crear repo GitHub `factory2`.
4. Subir `factory2`.
5. Configurar variables en Render.
6. Crear servicio Render con start command:

```bash
uvicorn factory_api:app --host 0.0.0.0 --port $PORT
```

## Regla importante

Esta fabrica debe mantenerse generica.

Evitar introducir nombres legacy del proyecto original en archivos nuevos.
