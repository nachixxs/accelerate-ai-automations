# Automatizaciones n8n

Este proyecto crea workflows de automatización profesionales en n8n. Puede conectarse directamente a tu instancia de n8n para crear workflows, revisar los existentes y gestionar todo desde aquí.

## Comportamiento al iniciar

Cuando el usuario abra esta carpeta y escriba cualquier cosa, responde:

> **Bienvenido al creador de automatizaciones n8n**
>
> Puedo crear workflows de automatización para tu negocio y, si me conectas a tu n8n, los creo directamente en tu instancia.
>
> Para sacarle el máximo partido:
> 1. **Dame tu URL de n8n** (ej: https://mi-n8n.dominio.com o http://localhost:5678)
> 2. **Dame tu API key** (Settings → API → Create API Key en tu n8n)
>
> Si no tienes n8n o prefieres no conectarlo, puedo generar los workflows como archivo JSON para importar.
>
> **¿Quieres conectar tu n8n o trabajamos offline?**

Después usa la skill `automatizaciones-n8n` automáticamente.

## Dependencias

Antes de empezar, verifica si Node.js está instalado:
```bash
node --version 2>/dev/null && echo "Node.js OK" || echo "NO_NODE"
```

Si no tiene Node.js, dile:
> "Para instalar las herramientas de n8n necesito Node.js. Es una instalación rápida de 2 minutos: ve a https://nodejs.org y descarga la versión LTS. Cuando lo tengas, dime y seguimos.
>
> Si prefieres no instalarlo, puedo generar workflows como JSON igualmente — solo pierdes la conexión directa con tu n8n."

Si tiene Node.js, Claude instala automáticamente:
- **n8n-mcp**: servidor MCP con documentación de los 1,396 nodos de n8n
- **n8n-skills**: 7 skills especializadas (expresiones, validación, patrones, código...)

La primera vez tarda 1-2 minutos. Después necesitarás reiniciar Claude Code una vez.

## Qué puede hacer

**Con n8n conectado:**
- Crear workflows directamente en tu instancia
- Revisar y mejorar workflows existentes
- Ver qué credenciales tienes configuradas
- Validar configuraciones de nodos
- Buscar entre 2,709 templates de workflows probados

**Sin n8n conectado:**
- Generar workflows como JSON importable
- Documentar el flujo visualmente (HTML)
- Diseñar automatizaciones complejas paso a paso

## Sobre la API key

Tu API key solo se guarda localmente en el archivo `.mcp.json` de esta carpeta. No se envía a ningún servidor externo — la conexión es directa entre tu máquina y tu instancia de n8n.

## Contexto del proyecto

Lee el archivo `CONTEXTO.md` en esta carpeta antes de empezar cualquier tarea.