# ⚡ Accelerate.ai — Kit de Automatizaciones n8n

![n8n](https://img.shields.io/badge/n8n-2.6.3-orange?style=flat-square&logo=n8n)
![Claude](https://img.shields.io/badge/Claude-Sonnet_4.6-6B48FF?style=flat-square&logo=anthropic)
![Workflows](https://img.shields.io/badge/workflows-1-brightgreen?style=flat-square)
![Status](https://img.shields.io/badge/status-active-success?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)
![LATAM](https://img.shields.io/badge/market-LATAM-red?style=flat-square)

Repositorio oficial de workflows de automatización con IA para la agencia **Accelerate.ai**.

Cada workflow está construido con **n8n + Claude (Anthropic)** y listo para importar en cualquier instancia de n8n.

---

## 🛠️ Stack

- **Motor de automatización:** n8n (self-hosted)
- **IA:** Claude Sonnet 4.6 (Anthropic API)
- **Base de datos:** Google Sheets
- **Email:** Gmail OAuth2
- **Mensajería:** WhatsApp Business API / Twilio

---

## 📁 Estructura

```
accelerate-ai-automations/
├── skills/                          # Skills especializadas para Claude Code
├── templates/                       # Prompts y templates reutilizables
├── workflows/
│   ├── lead-management/             # Calificación y seguimiento de leads
│   ├── whatsapp-bots/               # Bots de WhatsApp para negocios
│   └── reportes/                    # Reportes automáticos programados
└── docs/                            # Documentación visual de workflows
```

---

## 🤖 Workflows disponibles

| Workflow | Versión | Nicho | Estado |
|---|---|---|---|
| Calificador de Leads | v3 | Universal | ✅ Producción |
| WhatsApp Bot | v1 | Universal | 🔨 En construcción |

---

## 🚀 Cómo usar un workflow

1. Abrís tu n8n → **Workflows → Import from file**
2. Seleccionás el archivo `.json` del workflow
3. Configurás las credenciales necesarias (ver README de cada workflow)
4. Activás el workflow

---

## ⚙️ Credenciales necesarias

La mayoría de los workflows requieren:

- **Anthropic API Key** → [console.anthropic.com](https://console.anthropic.com)
- **Gmail OAuth2** → configurar en n8n Settings → Credentials
- **Google Sheets OAuth2** → configurar en n8n Settings → Credentials
- **WhatsApp Business API** → [Meta for Developers](https://developers.facebook.com)

---

## 🔒 Seguridad

El archivo `.mcp.json` contiene credenciales locales y está en `.gitignore` — nunca se sube a este repositorio.

---

## 📬 Contacto

**Nacho — Accelerate.ai**
- GitHub: [@nachixxs](https://github.com/nachixxs)
- LinkedIn: [Ignacio Noguerol](https://linkedin.com/in/ignacio-noguerol-54aa942b0)
