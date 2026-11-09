# Platemark MCP server

Platemark is a hosted MCP server that turns structured data into finished files: invoice, quote and receipt PDFs with the totals computed to the cent, certificates and letters, social images from templates, and short vertical videos.

Language models slip on arithmetic and page layout. Platemark takes both off their hands. The agent passes quantities and prices; Platemark does the math, formats money for the currency and locale, and returns a PDF link with the totals as JSON, so what the agent reports always matches the document.

This repository holds the listing files for MCP directories. The server itself is hosted, so there is nothing to install or run.

## Connect

Endpoint: `https://platemark.rowhousesoftware.com/mcp` (Streamable HTTP)

```json
{
  "mcpServers": {
    "platemark": {
      "type": "http",
      "url": "https://platemark.rowhousesoftware.com/mcp",
      "headers": { "Authorization": "Bearer pm_..." }
    }
  }
}
```

No key yet? Connect without the header and call `create_account` with an email. The agent gets a free key back.

## Tools

| Tool | What it does | Credits |
|-|-|-|
| `render_invoice` | Invoice PDF from line items, tax, discount, shipping and amount paid. Returns the link, page count and totals. | 2 |
| `render_document` | Quote, receipt, certificate or letter PDF. | 2 |
| `list_templates` | Image templates and their slots. Filter by tag, like `real estate`, `og` or `story`. | 0 |
| `render_image` | Fills a template and returns the PNG. Text shrinks to fit its box. | 1 |
| `account_status` | Plan and credits left. | 0 |
| `create_account` | Free account and API key, so an agent can sign itself up. | 0 |

## Example

What an agent sends to `render_invoice`:

```json
{
  "from": { "name": "Harbor Design Co.", "email": "billing@harbor.example" },
  "to": { "name": "Ledgerline, Inc." },
  "items": [
    { "description": "Website design", "quantity": 24, "unit_price": 65 },
    { "description": "Hosting, 12 months", "unit_price": 120 }
  ],
  "tax": { "percent": 6, "label": "Sales tax (6%)" },
  "due_days": 30
}
```

It gets back a link to the PDF and the totals Platemark used (subtotal 1,680.00, tax 100.80, total due 1,780.80).

## Pricing

Free: 100 credits a month with a small watermark. Paid plans start at $19 a month for 2,000 credits, with no watermark.

## Links

- Site: https://platemark.rowhousesoftware.com
- Docs: https://platemark.rowhousesoftware.com/docs
- Invoice guide: https://platemark.rowhousesoftware.com/guides/mcp-server-for-invoice-pdfs
- Official MCP registry: `com.rowhousesoftware/platemark`
- Support: support@rowhousesoftware.com
