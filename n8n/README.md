# WhatsApp Restaurant AI Agent (n8n)

This workflow creates a WhatsApp ordering assistant for a restaurant:

- Receives customer WhatsApp messages.
- Sends menu card text.
- Accepts order messages and places orders.
- Triggers either confirmation email task or confirmation call task.
- Creates a `Track ID` for each order.
- Tracks order status by `Track ID`.
- Returns the customer's last order.

## Import file

Import this file into n8n:

- `n8n/restaurant-whatsapp-agent.workflow.json`

## Required environment variables

Set these in your n8n instance before activating the workflow:

- `WHATSAPP_SEND_MESSAGE_URL` (Meta Cloud API endpoint to send messages)
- `WHATSAPP_ACCESS_TOKEN` (Bearer token for WhatsApp API)
- `CONFIRMATION_EMAIL_WEBHOOK_URL` (Your internal/email-service endpoint)
- `CONFIRMATION_CALL_WEBHOOK_URL` (Your internal/call-service endpoint)

## Example customer commands

- `menu`
- `order: 2x paneer tikka, 1x brownie`
- `track TRK-ABC123`
- `last order`
- `order: 1x veg biryani email` (forces email confirmation)

## Notes

- The workflow stores order state in n8n workflow static data (`global`), so track and last-order lookups work across executions in the same n8n instance.
- If the customer message includes `email` or `mail`, confirmation mode is email; otherwise it defaults to call.
- You can replace the intent-detection code node with an LLM node later if you want true model-based NLU.
