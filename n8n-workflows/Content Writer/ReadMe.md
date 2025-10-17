# Content Generator n8n Workflow

An AI-powered content creation system that generates high-quality, platform-optimized social media posts using strategic content planning and emotional psychology.

## Features

- 🎯 **Strategic Content Planning**: Multi-stage AI analysis for intentional content creation
- 🧠 **Psychology-Driven**: Incorporates emotional framing and audience psychology
- 📱 **Platform-Optimized**: Tailored content for different social media platforms
- 🎨 **Multiple Tone Options**: Raw & relatable, fun & bold, inspirational, professional, educational
- 🔄 **Structured Process**: Intent → Reasoning → Emotion → Outline → Final Content
- 📝 **Ready-to-Publish**: Generates complete posts with hooks, CTAs, and hashtags

## Content Creation Process

### 1. Intent Analysis
Identifies the core purpose and strategy behind your content:
- Target platform and audience
- Brand niche and industry
- Post type and objectives
- Tone and writing style

### 2. Strategic Reasoning
Analyzes the "why" behind the content:
- Key beliefs or pain points to address
- Myths or limiting mindsets to challenge
- Desired takeaways for readers
- Strategic thinking shifts to create value

### 3. Emotional Framing
Defines emotional connection strategy:
- Core emotions to evoke
- Emotional arc (pain → relief, stuck → empowered)
- Tone modifiers and voice
- Emotionally charged phrases

### 4. Content Outline
Creates structured post framework:
- Hook ideas (scroll-stopping openers)
- Story or concept summary
- Pivot points or punchlines
- CTA strategies
- Hashtag themes

### 5. Final Content Generation
Produces ready-to-publish content using GPT-4O with:
- Strong opening hooks
- Natural rhythm and flow
- Platform-specific formatting
- Engaging CTAs
- 3-5 trending, niche-relevant hashtags

## Usage

### API Request Format
```bash
curl -X POST https://your-n8n-instance.com/webhook/e93740ce-c11a-411b-9b86-856d0d75a328 \
  -H "Content-Type: application/json" \
  -d '{
    "Topic": "productivity tips for remote workers",
    "Platform": "LinkedIn",
    "Tone": "Professional"
  }'
```

### Input Parameters
- **Topic** (required): The subject or theme for your content
- **Platform** (required): Target social media platform (LinkedIn, Instagram, Twitter, etc.)
- **Tone** (required): Desired tone and writing style

### Available Tones

#### Raw & Relatable
- **Style**: Unfiltered, personal, messy-in-a-good-way
- **Best for**: Building authentic connections, vulnerability posts

#### Fun & Bold  
- **Style**: Confident, witty, rebellious
- **Best for**: Entertainment, brand personality, engagement

#### Inspirational
- **Style**: Uplifting, purpose-driven, emotional
- **Best for**: Motivation, leadership, personal development

#### Professional
- **Style**: Polished, value-rich, LinkedIn-style
- **Best for**: Business insights, thought leadership, B2B content

#### Educational
- **Style**: Informative, clear, helpful
- **Best for**: How-to content, tutorials, industry knowledge

## Example Output

**Input:**
```json
{
  "Topic": "overcoming imposter syndrome",
  "Platform": "LinkedIn", 
  "Tone": "Raw & Relatable"
}
```

**Generated Content:**
```
That voice in your head saying "you don't belong here"?

I used to think it would go away when I got more experienced.
When I had more credentials.
When I finally "made it."

Plot twist: It never fully disappears.

The difference isn't silencing imposter syndrome.
It's learning to work alongside it.

Now when that voice shows up, I acknowledge it:
"Thanks for trying to protect me, but I've got this."

Your expertise isn't measured by the absence of doubt.
It's measured by your willingness to show up despite it.

What's one thing imposter syndrome has been whispering to you lately?

#ImpostorSyndrome #Leadership #PersonalGrowth #Authenticity #ProfessionalDevelopment
```

## Response Format

The workflow returns formatted HTML content ready for publishing:

```json
{
  "html": "<p>Your formatted social media post content...</p>",
  "originalText": "Raw markdown version of the content"
}
```

## Setup Instructions

### Prerequisites
- n8n instance with LangChain nodes
- OpenAI API key with access to GPT-4O and GPT-4.1-mini

### Configuration Steps

1. **Import Workflow**: Import the workflow JSON into your n8n instance

2. **Configure OpenAI Credentials**: 
   - Set up your OpenAI API credentials in n8n
   - Ensure access to GPT-4O and GPT-4.1-mini models

3. **Activate Webhook**: 
   - Enable the workflow to activate the webhook endpoint
   - Note the webhook URL for API calls

4. **Test Content Generation**:
   ```bash
   curl -X POST [your-webhook-url] \
     -H "Content-Type: application/json" \
     -d '{"Topic": "test topic", "Platform": "LinkedIn", "Tone": "Professional"}'
   ```

## AI Model Usage

- **GPT-4.1-mini**: Used for intent analysis, reasoning, emotional framing, and outline creation
- **GPT-4O**: Used for final content generation with optimized creativity settings
- **Temperature Settings**: Carefully tuned for each stage (0.4 for analysis, 0.9 for creation)

## Content Quality Features

- **Hook Optimization**: Creates scroll-stopping opening lines
- **Rhythm & Flow**: Uses natural line breaks and pacing
- **Platform Awareness**: Adapts format and style for each platform
- **Hashtag Strategy**: Generates relevant, trending hashtags (avoids generic tags)
- **CTA Optimization**: Creates engaging calls-to-action for interaction

## Use Cases

- **Content Creators**: Streamline social media content production
- **Marketing Teams**: Generate platform-specific marketing content
- **Personal Brands**: Create authentic, engaging personal content
- **Agencies**: Scale content creation for multiple clients
- **Thought Leaders**: Develop strategic, value-driven posts

## Performance Optimization

- **Multi-stage Processing**: Ensures strategic depth and quality
- **Model Selection**: Uses appropriate AI models for each task
- **Bot Protection**: Webhook configured to ignore bot traffic
- **Response Optimization**: Markdown to HTML conversion for clean output

---

*Built for professional content creators using n8n workflow automation*