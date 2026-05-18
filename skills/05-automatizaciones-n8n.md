---
name: automatizaciones-n8n
description: "Crea, revisa y gestiona workflows de automatización en n8n. Conecta con tu instancia de n8n para crear workflows directamente, revisar los existentes, y automatizar cualquier proceso de negocio. Usa esta skill cuando el usuario quiera automatizar procesos, crear workflows en n8n, revisar automatizaciones existentes, conectar herramientas, o cualquier cosa relacionada con n8n. Triggers: 'automatiza esto', 'workflow de n8n', 'automatización', 'conectar herramientas', 'automatizar emails/leads/redes', 'revisa mis workflows', 'crea una automatización', 'n8n'."
---

# Automatizaciones n8n

Creas workflows de automatización profesionales en n8n. Puedes conectarte a la instancia del usuario para crear workflows directamente, revisar los existentes, y generar documentación visual.

**Regla fundamental: pregunta antes de ejecutar.** No crees ni modifiques workflows en la instancia del usuario sin su confirmación explícita.

---

## Paso 0 — Verificar e instalar dependencias

Antes de empezar, verifica que el MCP de n8n y las skills están disponibles. Si no lo están, instálalos automáticamente.

### Verificar MCP n8n

Comprueba si las herramientas del MCP de n8n están disponibles (busca tools como `get_node`, `search_nodes`, `list_workflows`, etc.). Si no están:

> "Para trabajar con n8n necesito instalar un par de cosas. Dame un momento (30-60 segundos la primera vez)."

```bash
# Instalar el MCP server de n8n globalmente
npm install -g n8n-mcp 2>/dev/null || npm install n8n-mcp
```

Después configura el MCP en el settings del proyecto. Crea o actualiza `.mcp.json` en la raíz del proyecto:

```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true"
      }
    }
  }
}
```

Avisa al usuario que necesita reiniciar Claude Code para que el MCP se active.

### Verificar skills de n8n

Comprueba si las skills de n8n están instaladas (n8n-expression-syntax, n8n-workflow-patterns, etc.). Si no:

```bash
# Clonar e instalar skills de n8n
git clone https://github.com/czlonkowski/n8n-skills.git /tmp/n8n-skills
mkdir -p ~/.claude/skills
cp -r /tmp/n8n-skills/skills/* ~/.claude/skills/
rm -rf /tmp/n8n-skills
```

---

## Paso 1 — Conectar con n8n (opcional pero recomendado)

Pregunta al usuario si tiene una instancia de n8n y quiere conectarla:

> "¿Tienes una instancia de n8n funcionando? Si me das la URL y tu API key, puedo:
> - Crear workflows directamente en tu n8n
> - Revisar y mejorar tus workflows existentes
> - Ver qué credenciales tienes configuradas
>
> Si no tienes n8n o prefieres no conectarlo, puedo generar los workflows como archivo JSON para que los importes manualmente.
>
> **¿Tu URL de n8n?** (ej: https://mi-n8n.dominio.com o http://localhost:5678)
> **¿Tu API key?** (la encuentras en Settings → API → Create API Key)"

Si el usuario proporciona URL + API key:

1. Actualiza `.mcp.json` añadiendo las credenciales:
```json
{
  "mcpServers": {
    "n8n-mcp": {
      "command": "npx",
      "args": ["n8n-mcp"],
      "env": {
        "MCP_MODE": "stdio",
        "LOG_LEVEL": "error",
        "DISABLE_CONSOLE_OUTPUT": "true",
        "N8N_API_URL": "[URL del usuario]",
        "N8N_API_KEY": "[API key del usuario]"
      }
    }
  }
}
```

2. Avisa que necesita reiniciar Claude Code

3. Una vez conectado, verifica que funciona listando los workflows existentes

**Si el usuario no quiere conectar n8n**: trabaja en modo offline — genera JSONs importables y documentación.

---

## Paso 2 — Entender qué automatizar

### Si el usuario tiene n8n conectado

Primero explora lo que ya tiene:
- Lista sus workflows existentes
- Revisa las credenciales que tiene configuradas (esto te dice qué herramientas usa)
- Pregunta qué quiere mejorar, crear, o qué procesos manuales tiene

### Si trabaja desde cero

Pregunta:
- **¿Qué quieres automatizar?** — describe el proceso manual que haces hoy
- **¿Qué herramientas usas?** — Gmail, Google Sheets, Slack, Notion, CRM, Stripe, WhatsApp, WordPress, etc.
- **¿Cuál es el disparador?** — qué evento inicia el proceso (llega un email, alguien rellena un formulario, cada día a las 9h, alguien paga, etc.)
- **¿Qué debe pasar paso a paso?** — el flujo completo

Si el usuario no sabe qué automatizar, proponle ideas basadas en su negocio:

**Para agencias/consultorías:**
- Captación de leads: formulario web → CRM + email de bienvenida + Slack
- Seguimiento automático: si el lead no responde en 3 días → email de follow-up
- Onboarding de cliente: pago recibido → crear carpeta Drive + enviar accesos + tarea en Notion

**Para ecommerce:**
- Pedido nuevo → confirmar stock + enviar email + actualizar inventario
- Review negativa → alerta a Slack + respuesta automática
- Carrito abandonado → email de recordatorio a las 24h

**Para creadores de contenido:**
- Planificación: Google Sheets con calendario → publicar en LinkedIn + Twitter + Telegram
- Nuevo suscriptor → email de bienvenida + añadir a lista + notificar

---

## Paso 3 — Diseñar y crear el workflow

### Usa las herramientas del MCP

Si el MCP de n8n está disponible, úsalo para:
- **Buscar nodos** correctos para cada herramienta (search_nodes)
- **Consultar documentación** de cada nodo (get_node) — propiedades, operaciones, campos requeridos
- **Buscar templates** similares a lo que necesita el usuario (search_templates)
- **Validar el workflow** antes de crearlo

### Usa las skills de n8n

Si las skills están instaladas, aplícalas:
- **n8n-expression-syntax** para escribir expresiones correctas ({{ $json.field }})
- **n8n-workflow-patterns** para elegir el patrón arquitectónico correcto
- **n8n-node-configuration** para configurar nodos correctamente
- **n8n-validation-expert** si hay errores de validación
- **n8n-code-javascript/python** si necesitas nodos de código

### Crear el workflow

**Si tiene n8n conectado:** crea el workflow directamente en su instancia con la API. Muéstrale el resultado y pregunta si quiere activarlo.

**Si no tiene n8n conectado:** genera un archivo `workflow-[nombre].json` válido para importar.

En ambos casos:
- Posiciona los nodos de forma legible (flujo de izquierda a derecha, 250px entre nodos)
- Nombra cada nodo de forma descriptiva (no "HTTP Request" sino "Obtener datos del lead")
- Añade notas/sticky notes explicando las partes clave
- Configura manejo de errores (Error Trigger + notificación)

---

## Paso 4 — Documentar el workflow

Genera un archivo HTML con la documentación visual del workflow:

### Contenido

1. **Nombre y descripción** del workflow
2. **Diagrama visual del flujo** — representación con cajas y flechas (HTML/CSS puro) mostrando cada nodo y las conexiones
3. **Configuración paso a paso** — qué configurar en cada nodo
4. **Credenciales necesarias** — lista de API keys/OAuth que necesita
5. **Datos de ejemplo** — qué entra y qué sale en cada paso
6. **Cómo importar en n8n** — si se generó como JSON, instrucciones claras:
   - Abre n8n → Workflows → Import from file
   - Selecciona el archivo JSON
   - Configura las credenciales en cada nodo
   - Activa el workflow

### Diseño

Libertad creativa total. El diagrama debe ser claro y visualmente atractivo.

---

## Paso 5 — Revisar workflows existentes (si tiene n8n conectado)

Si el usuario pide revisar un workflow existente:

1. Lee el workflow de su instancia
2. Analiza:
   - ¿Los nodos están bien configurados?
   - ¿Las expresiones son correctas?
   - ¿Hay manejo de errores?
   - ¿El flujo es eficiente o hay pasos innecesarios?
   - ¿Hay riesgos de seguridad? (API keys en texto plano, webhooks sin auth, etc.)
3. Propón mejoras concretas
4. Si el usuario acepta, aplica los cambios directamente

---

## Paso 6 — Presentar el resultado

Muestra:

1. Nombre del workflow creado/modificado
2. Diagrama resumido del flujo (texto)
3. Credenciales que necesita configurar
4. Si está conectado: link directo al workflow en su n8n
5. Si es JSON: nombre del archivo + instrucciones de importación
6. Documentación generada
7. Pregunta si quiere ajustar algo

No muestres precios sugeridos ni consejos de venta.
