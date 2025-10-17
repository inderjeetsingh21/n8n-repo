# Magic Hour AI - API Testing Interface

A web-based testing interface for Magic Hour AI's image generation and text-to-video APIs with n8n integration.

## Features

- **AI Image Generator** - Generate 1-4 images with 40+ style tools
- **Text-to-Video** - Create 5-60 second videos in 480p/720p/1080p
- **n8n Integration** - Direct webhook support
- **Code Generation** - Auto-generate cURL, Python, JavaScript, n8n configs
- **Real-time Monitoring** - Automatic status polling and results display

## Quick Start

1. Download `magichour-api-tester.html`
2. Open in browser
3. Enter your n8n webhook URL
4. Start generating!

## n8n Workflow Setup
```
Webhook → HTTP Request (POST) → Wait (300s) → HTTP Request (GET) → Respond to Webhook
```

**Critical**: Return JSON metadata, NOT binary files!

### Expected Response Format
```json
{
  "status": "complete",
  "id": "project-id",
  "downloads": [{"url": "https://cdn.magichour.ai/..."}],
  "credits_charged": 5
}
```

## API Endpoints
```bash
# Image Generation
POST https://api.magichour.ai/v1/ai-image-generator

# Text-to-Video
POST https://api.magichour.ai/v1/text-to-video

# Status Check
GET https://api.magichour.ai/v1/image-projects/{id}
GET https://api.magichour.ai/v1/video-projects/{id}
```

## Pricing

**Images**: 5 credits per image (max 4 per request)

**Videos**:
- 480p: 120 credits/5s
- 720p: 300 credits/5s  
- 1080p: 600 credits/5s

## Example Usage

### Image Generation
```json
{
  "name": "Mountain Sunset",
  "image_count": 2,
  "orientation": "landscape",
  "style": {
    "prompt": "Serene landscape with mountains and sunset",
    "tool": "ai-landscape-generator"
  }
}
```

### Video Generation
```json
{
  "name": "Dog Running",
  "end_seconds": 5,
  "resolution": "720p",
  "orientation": "landscape",
  "style": {
    "prompt": "A dog running through flowers"
  }
}
```

## Requirements

- Modern web browser
- Magic Hour AI API key
- n8n instance (for webhook integration)

## Troubleshooting

**"Server returned non-JSON response"**  
→ Check n8n workflow returns JSON, not binary data

**"Failed to send request"**  
→ Verify webhook URL and n8n instance status

**"Timeout"**  
→ Check API credits and workflow logs

## Documentation

- [Magic Hour AI Docs](https://docs.magichour.ai)
- [API Reference](https://api.magichour.ai/docs)
- [n8n Documentation](https://docs.n8n.io)

## License

MIT License

---

**Made with ❤️ for the Magic Hour AI community**