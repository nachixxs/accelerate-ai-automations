# Contexto del Proyecto — Accelerate.ai

Lee este archivo completo antes de empezar cualquier tarea.

---

## Quién soy

Soy Nacho, 20 años, General Alvear, Mendoza, Argentina. Tengo una agencia de automatizaciones con IA llamada **Accelerate.ai**. Construyo automatizaciones para pymes locales y latinoamericanas usando n8n + Claude como stack principal.

---

## n8n — Configuración actual

- **URL:** http://localhost:5678
- **API Key:** configurada en `.mcp.json`
- **Versión:** 2.6.3
- **Modo:** self-hosted local (no cloud)

Al iniciar, preguntame siempre: "¿Confirmás que n8n está corriendo en http://localhost:5678 con la API key configurada?" — esperá mi confirmación antes de continuar. Esto es para verificar que leíste el contexto correctamente.

---

## Stack de trabajo

- **Motor:** n8n (localhost:5678)
- **IA:** Claude API (Anthropic) — modelo **Claude Sonnet 4.6** (`claude-sonnet-4-6`)
- **Base de datos:** Google Sheets (para leads y clientes)
- **Email:** Gmail (OAuth)
- **WhatsApp:** WhatsApp Business API / Twilio como alternativa
- **Código:** Claude Code + Skills de Adrián Sáenz
- **OS:** Windows 11, PowerShell

---

## Automatizaciones ya construidas (usar como referencia)

### Demo 1 v3 — Calificador de Leads (REFERENCIA BASE)
- **Archivo:** `workflows/lead-management/Demo_1_Calificador_Leads_v3.json`
- **Flujo:** Webhook → recibe lead → Claude califica (CALIENTE/TIBIO/FRÍO) → guarda en Google Sheets → email personalizado al lead → alerta al dueño según clasificación → Error Trigger para fallos
- **Estado:** funcionando, es la referencia de estructura y calidad para todo lo que construyas
- **Patrón:** usar siempre este JSON como base estructural para nuevas automatizaciones
- **Mejoras vs v2:** notificación para leads TIBIOS, Error Trigger configurado, manejo completo de los 3 estados

---

## Nichos prioritarios de la agencia

En orden de prioridad para los próximos meses:

1. **Gastronomía / Restaurantes** — bots de reservas WhatsApp, seguimiento de clientes
2. **Salud / Clínicas / Odontología** — agenda de turnos, recordatorios automáticos
3. **Real Estate / Inmobiliarias** — calificación de leads, seguimiento automático
4. **Servicios profesionales** — agenda, follow-up, propuestas automáticas
5. **E-commerce** — recuperación de carritos, notificaciones de envío

---

## Patrones preferidos

Cuando construyas automatizaciones, priorizá estos patrones:

- **Base de datos:** Google Sheets (no Airtable, no Notion — el cliente ya lo conoce)
- **Email:** Gmail OAuth (no SMTP genérico)
- **WhatsApp:** WhatsApp Business API como primera opción, Twilio como fallback
- **IA:** siempre Claude Sonnet 4.5 — no GPT, no Gemini dentro de los workflows
- **Trigger principal:** Webhook para tiempo real, Schedule para reportes
- **Notificación al dueño:** siempre incluir al final del workflow (Gmail o WhatsApp)
- **Manejo de errores:** siempre incluir Error Trigger con notificación

---

## Estructura de un workflow bien hecho

Todo workflow que construyas debe tener:

1. **Trigger claro** — Webhook o Schedule, bien nombrado
2. **Limpieza de datos** — nodo Set para formatear antes de procesar
3. **Lógica de Claude** — system prompt específico del nicho del cliente
4. **Almacenamiento** — Google Sheets con las columnas correctas
5. **Acción principal** — email, WhatsApp, o lo que corresponda
6. **Notificación al dueño** — siempre al final
7. **Manejo de errores** — Error Trigger configurado
8. **Nodos bien nombrados** — en español, descriptivos (no "HTTP Request" sino "Obtener datos del lead")

---

## Cómo nombrá los archivos JSON

```
Demo_[número]_-_[Nombre_Descriptivo]_v[versión].json
```

Ejemplos:
- `Demo_1_-_Calificador_de_Leads_v2.json`
- `Demo_2_-_WhatsApp_Bot_v1.json`
- `Demo_3_-_Reporte_Semanal_v1.json`

---

## Lo que NO hacer

- No usar Airtable ni Notion como base de datos (el cliente no los conoce)
- No usar GPT ni otros modelos — solo **Claude Sonnet 4.6** (`claude-sonnet-4-6`)
- No crear workflows sin manejo de errores
- No dejar nodos con nombres genéricos ("Webhook", "Set", "IF")
- No preguntar la URL ni la API key de n8n — ya están en `.mcp.json`
- No mostrar precios ni sugerencias de venta
- No crear workflows de más de 25 nodos — si es muy complejo, dividir en sub-workflows

---

## Meta inmediata

Primer cliente pago antes del 30 de junio 2026. Cada automatización que construyas debe ser lo suficientemente sólida para ser entregada a un cliente real.