# Accelerate.ai automations

n8n workflows and prompt templates used as demos by Accelerate.ai, my AI automation agency. Each workflow is an exported n8n JSON file you can import into your own instance. Prompts, emails and node names are in Spanish.

## Workflows

### Lead qualifier (v3)

File: [`workflows/lead-management/Demo_1_-_Calificador_de_Leads_v3.json`](workflows/lead-management/Demo_1_-_Calificador_de_Leads_v3.json)

- **Trigger:** `POST /leads` webhook with `nombre`, `email` and `mensaje` in the body.
- **Classification:** an n8n AI Agent node with the Anthropic chat model (Claude Sonnet 4.5) reads the message and returns JSON: `clasificacion` (`CALIENTE` / `TIBIO` / `FRÍO`: hot, warm, cold), name, interest, urgency, recommended action and a suggested reply to the lead. A Code node strips stray markdown fences and parses that JSON.
- **Storage:** appends a row to Google Sheets (date, name, classification, interest, urgency, recommended action, reply, original message).
- **Reply:** sends the lead an email through Gmail, with a subject that depends on the classification.
- **Routing:** hot leads trigger an urgent HTML email to the business owner, warm leads a follow-up email; cold leads are only stored. The webhook then answers `OK`.
- **Errors:** a separate Error Trigger branch formats the failed node and error message and emails an alert.

The folder's [README](workflows/lead-management/README.md) (Spanish) has a test payload and setup details.

### WhatsApp bot (placeholder)

`workflows/whatsapp-bots/Demo_2_WhatsApp_Bot_v1.json` is an empty placeholder. There is no WhatsApp workflow in this repo yet.

## Other files

- [`templates/prompt-templates.md`](templates/prompt-templates.md): system prompts for lead qualification (generic, restaurants, clinics, real estate), a conversational WhatsApp bot and a weekly report generator.
- [`skills/05-automatizaciones-n8n.md`](skills/05-automatizaciones-n8n.md): a Claude Code skill for designing and reviewing n8n workflows through the n8n MCP server.

## How to import

1. In n8n: **Workflows > Import from file** and pick the JSON.
2. Create your own credentials (Anthropic API, Gmail OAuth2, Google Sheets OAuth2) and select them in the nodes. The Gmail nodes ship with a `REEMPLAZAR_CON_TU_CREDENTIAL_ID` placeholder.
3. Point the "Guardar en Sheets" node to your own spreadsheet and change the recipient address in the owner alert nodes.
4. The Error Trigger only fires if this workflow is selected as an error workflow (Workflow settings > Error workflow); the export does not set one.
5. Activate the workflow and send a test `POST` to the webhook.

## Stack

n8n (self-hosted), Claude via the n8n Anthropic node, Google Sheets, Gmail.

## Contact

Ignacio Noguerol, [@nachixxs](https://github.com/nachixxs)
