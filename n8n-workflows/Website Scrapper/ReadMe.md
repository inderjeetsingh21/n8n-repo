# Website Scraper n8n Workflow

An intelligent website scraping workflow that extracts data from web pages and formats it using AI according to your specific requirements.

## Features

- 🤖 **AI-Powered Formatting**: Uses OpenAI GPT-4 to format scraped data according to custom prompts
- 🔍 **Smart Data Extraction**: Extracts titles, content, links, and images from web pages
- 🛡️ **Robots.txt Compliance**: Automatically checks and respects robots.txt rules
- 📝 **Custom Selectors**: Supports custom CSS selectors for targeted data extraction
- 🌐 **Webhook Integration**: Can be triggered via webhook or workflow execution
- ✅ **Input Validation**: Validates URLs and required parameters before processing

## Usage

### Via Webhook (POST)
```bash
curl -X POST https://your-n8n-instance.com/webhook/scrape-website \
  -H "Content-Type: application/json" \
  -d '{
    "url": "https://example.com",
    "userPrompt": "Extract the main article title and content as a clean JSON object",
    "selectors": {
      "title": "h1, title",
      "content": "article, .content",
      "links": "a[href]",
      "images": "img[src]"
    }
  }'
```

### Via Workflow Execution
Execute the workflow with these inputs:
- `url`: Target website URL (required)
- `userPrompt`: Instructions for AI formatting (required)
- `title`: CSS selector for title elements
- `content`: CSS selector for content elements
- `links`: CSS selector for links
- `images`: CSS selector for images

## Response Format

```json
{
  "success": true,
  "data": {
    // AI-formatted data based on your prompt
  },
  "metadata": {
    "scrapedUrl": "https://example.com",
    "scrapedAt": "2025-07-20T06:08:26.000Z",
    "robotsInfo": "Robots.txt found and analyzed",
    "userPrompt": "Your formatting instructions",
    "aiFormatted": true
  }
}
```

## Setup

1. Import the workflow into your n8n instance
2. Configure OpenAI credentials for the AI Formatting node
3. Activate the workflow
4. Use the webhook endpoint or execute manually

## Error Handling

- Validates URL format and required parameters
- Checks robots.txt compliance before scraping
- Provides fallback formatting if AI processing fails
- Returns detailed error messages for troubleshooting

## Dependencies

- OpenAI API key for AI formatting
- n8n instance with webhook support
- Active internet connection for scraping

---