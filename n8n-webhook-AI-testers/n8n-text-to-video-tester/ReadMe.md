# Text to Video Generation Test UI

A modern, user-friendly web interface for testing n8n workflows that generate AI-powered videos. 
This HTML interface cane be used for sending video generation requests to your n8n webhook endpoint with real-time progress tracking and streaming support.

## 🚀 Quick Start

1. **Update the Webhook URL** in the HTML file (line 452):
   ```javascript
   const webhookUrl = 'YOUR_N8N_WEBHOOK_URL';
   ```

2. **Open the HTML file** in any modern web browser

3. **Fill in the form** and click "Generate Video"

## 📥 Input Requirements

The UI sends a POST request to your n8n webhook with the following JSON payload:

```json
{
  "prompt": "string (required)",
  "imageUrl": "string (optional)",
  "aspectRatio": "string (required)",
  "duration": "number (required)",
  "quality": "string (required)",
  "waterMark": "string (optional)"
}
```

### Validation Rules

⚠️ **Important Constraints:**
- 10-second videos **cannot** use 1080p quality
- 1080p quality **cannot** generate 10-second videos
- Only 5-second videos can use 1080p quality

## 📤 Output Requirements (n8n Webhook Response)

Your n8n webhook must return data in one of the following formats:

### Option 1: JSON Response with Video URL

```json
{
  "videoUrl": "https://example.com/generated-video.mp4"
}
```

**Use Case:** When the video is hosted and you return a URL to access it

### Option 2: JSON Response with Error

```json
{
  "error": "Error message describing what went wrong"
}
```


## 🔧 n8n Workflow Setup

Your n8n workflow should include:

1. **Webhook Node** - Trigger node to receive POST requests
   - Method: POST
   - Path: `/webhook/generate-image` (or your custom path)
   - Response Mode: 
     - "Respond Immediately" for JSON responses
     - "When Last Node Finishes" for binary streaming

2. **AI Video Generation Node** - Your video generation service (Runway, Stable Diffusion, etc.)

3. **Response Node** - Return data in one of the supported formats:
   ```javascript
   // Option 1: Return video URL
   return {
     json: {
       videoUrl: "https://cdn.example.com/video.mp4"
     }
   };
   
   // Option 2: Return binary data
   return {
     binary: {
       data: videoBuffer
     }
   };
   
   // Option 3: Return error
   return {
     json: {
       error: "Video generation failed: API limit reached"
     }
   };
   ```

## 📋 Example Request

```bash
curl -X POST https://your-n8n-instance.com/webhook/generate-image \
  -H "Content-Type: application/json" \
  -d '{
    "prompt": "A cheerful young boy sitting on a tree stump in a sunny forest, gently holding a curious chipmunk in his hands.",
    "imageUrl": "",
    "aspectRatio": "16:9",
    "duration": 5,
    "quality": "1080p",
    "waterMark": ""
  }'
```

## 🎨 Customization

### Update Webhook URL
Line 393:
```javascript
const webhookUrl = 'https://your-n8n-instance.com/webhook/your-path';
```

### Modify Available Options
Update the `<select>` elements in the HTML:
```html
<select id="aspectRatio" name="aspectRatio" required>
    <option value="16:9">16:9 (Horizontal)</option>
    <option value="9:16">9:16 (Vertical)</option>
    <option value="1:1">1:1 (Square)</option>
    <!-- Add more options -->
</select>
```

### Change Default Values
Line 548:
```javascript
document.getElementById('prompt').value = 'Your default prompt here';
```

## 🐛 Error Handling

The UI handles errors gracefully:

- **Network Errors** - Displays connection issues
- **HTTP Errors** - Shows status code and error message
- **Validation Errors** - Prevents invalid combinations before submission
- **API Errors** - Displays error messages returned by your webhook

## 🌐 Browser Compatibility

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+

## 📝 License

This is a test/demo interface. Customize and use according to your needs.

## 🤝 Contributing

Feel free to submit issues, fork the repository, and create pull requests for any improvements.

---

**Note:** This UI is designed to work with n8n workflows. Ensure your n8n instance is properly configured and the webhook endpoint is accessible from the client's browser.