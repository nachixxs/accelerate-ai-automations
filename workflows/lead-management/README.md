# 📋 Demo 1 — Calificador de Leads v3

Workflow que recibe leads via webhook, los califica con Claude y notifica al dueño del negocio según la urgencia.

---

## ¿Qué hace?

```
Webhook recibe lead (nombre, email, mensaje)
        ↓
Claude Sonnet 4.6 califica el lead
        ↓
Guarda en Google Sheets con todos los datos
        ↓
Envía email personalizado al lead
        ↓
IF CALIENTE → email HTML urgente al dueño 🔴
IF TIBIO    → email HTML de seguimiento al dueño 🟡
IF FRÍO     → solo queda guardado en Sheets 🟢
        ↓
Error Trigger → alerta si algo falla ⚠️
```

---

## Clasificación de leads

| Clasificación | Criterio | Acción del dueño |
|---|---|---|
| 🔴 CALIENTE | Quiere comprar pronto, pregunta precios | Contactar hoy |
| 🟡 TIBIO | Interesado sin urgencia | Seguimiento esta semana |
| 🟢 FRÍO | Solo curiosidad | Solo registrar |

---

## Credenciales necesarias

| Credencial | Nodos que la usan | Cómo configurar |
|---|---|---|
| **Anthropic API** | AI Agent | Settings → Credentials → Anthropic |
| **Gmail OAuth2** | Email al Lead, Alerta al Dueño, Alerta TIBIO, Alerta Error | Settings → Credentials → Gmail OAuth2 |
| **Google Sheets OAuth2** | Guardar en Sheets | Settings → Credentials → Google Sheets |

---

## Cómo importar

1. `Workflows → Import from file`
2. Seleccionás `Demo_1_Calificador_Leads_v3.json`
3. Reemplazás `REEMPLAZAR_CON_TU_CREDENTIAL_ID` con tu ID real de Gmail en los 4 nodos de Gmail
4. Actualizás el ID de tu Google Sheet en el nodo "Guardar en Sheets"
5. Activás el workflow

---

## Cómo probarlo

Mandás un POST al webhook con este body:

```json
{
  "nombre": "Juan Pérez",
  "email": "juan@test.com",
  "mensaje": "Hola, quiero contratar sus servicios cuanto antes, tengo presupuesto disponible"
}
```

Resultado esperado:
- Lead guardado en Google Sheets
- Email de respuesta enviado a juan@test.com
- Email 🔴 CALIENTE enviado a tu Gmail

---

## Formato condicional en Google Sheets

En la columna **Clasificacion**:
- 🔴 CALIENTE → fondo `#ea4335`
- 🟡 TIBIO → fondo `#fbbc04`
- 🟢 FRÍO → fondo `#34a853`