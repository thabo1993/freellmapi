# FreeLLMAPI - LLM Providers Reference

This document lists all the LLM providers available through FreeLLMAPI, including their signup URLs, available models, and key features.

---

## Provider Overview

| Provider | Signup URL | Models | Key Strength |
|----------|-----------|--------|--------------|
| Google AI Studio | ai.google.dev | Gemini 2.5, 1.5 | Most Capable |
| Grok | console.groq.com | Llama, Mixtral, Grok | Blazing Fast |
| GitHub Models | github.com | GPT-4o and more | Premium Quality |
| Cerebras | cloud.cerebras.ai | Llama 3.1 | Very Fast Inference |
| Nvidia | build.nvidia.com | Nemotron | Enterprise Ready |
| Mistral | console.mistral.ai | Large, Medium | Fast & Capable |
| OpenRouter | openrouter.ai | 100+ models | Maximum Variety |
| Hugging Face | huggingface.co | Multiple models | Community Driven |
| Meta | (via OpenRouter) | Llama series | Open Source Quality |

---

## Detailed Provider Guides

### 1. Google AI Studio (Gemini)

**Signup URL:** https://ai.google.dev

**Available Models:**
- Gemini 2.5 Flash (Recommended - Most Capable)
- Gemini 1.5 Pro
- Gemini 1.5 Flash
- Gemini 1.0 Pro

**Key Features:**
- Most capable free model available
- High context window
- Multimodal support (text, images)
- Excellent reasoning capabilities
- Recommended as first priority in fallback chain

**Setup Steps:**
1. Go to https://ai.google.dev
2. Sign in with your Google account
3. Click **Get API Key**
4. Click **Create API Key**
5. Optionally name it `free-llm-api`
6. Choose an existing project or create a new one
7. Copy the API key
8. Paste into FreeLLMAPI dashboard under "Google AI Studio"

**Free Tier Limits:**
- Generous token limits
- Suitable for most development projects
- High daily request limits

---

### 2. Grok (Groq)

**Signup URL:** https://console.groq.com

**Available Models:**
- Llama 3.1 (Various sizes)
- Mixtral 8x7B
- Grok-1
- Grok-2

**Key Features:**
- Fastest inference speeds available
- Ideal for latency-sensitive applications
- Excellent for real-time applications
- Reliable and very fast token generation

**Setup Steps:**
1. Go to https://console.groq.com
2. Sign up for a free account
3. Navigate to **API Keys**
4. Click **Create API Key**
5. Copy the key
6. Paste into FreeLLMAPI dashboard under "Grok"

**Free Tier Limits:**
- Millions of tokens per month
- Very fast response times
- Recommended as second priority in fallback chain

**Recommended Use Case:**
- Use when you need speed
- Set as fallback when Gemini unavailable
- Great for streaming responses

---

### 3. GitHub Models

**Signup URL:** https://github.com

**Available Models:**
- GPT-4o
- GPT-4 Turbo
- Claude models (via GitHub)
- Llama models

**Key Features:**
- Access to GPT-4o (premium model)
- Free tier for GitHub users
- OAuth integration with GitHub
- Professional-grade models

**Setup Steps:**
1. Go to https://github.com
2. Sign in (or create account)
3. Click your **profile picture** → **Settings**
4. Go to **Developer Settings** → **Personal Access Tokens**
5. Click **Generate New Token**
6. Give it a name (e.g., "freellmapi")
7. Set expiration to **No Expiration**
8. Click **Generate Token**
9. Copy the token
10. Paste into FreeLLMAPI dashboard under "GitHub Models"

**Free Tier Limits:**
- Free tier includes GPT-4o access
- Good monthly token limits
- Recommended as third priority in fallback chain

**Recommended Use Case:**
- When you need GPT-4o quality
- Fallback when Gemini and Grok are busy

---

### 4. Cerebras

**Signup URL:** https://cloud.cerebras.ai

**Available Models:**
- Llama 3.1 (70B)
- Llama 3.1 (8B)

**Key Features:**
- Extremely fast inference
- Wafer-scale AI architecture
- Good for high-throughput applications
- Reliable and scalable

**Setup Steps:**
1. Go to https://cloud.cerebras.ai
2. Sign up for free
3. Navigate to **API Keys**
4. Create a new API key
5. Copy the key
6. Paste into FreeLLMAPI dashboard under "Cerebras"

**Free Tier Limits:**
- Good token allowance
- Very fast response times
- Good reliability

---

### 5. Nvidia

**Signup URL:** https://build.nvidia.com

**Available Models:**
- Nemotron (various versions)
- Llama models

**Key Features:**
- Enterprise-grade infrastructure
- Optimized for Nvidia hardware
- Professional support
- High reliability

**Setup Steps:**
1. Go to https://build.nvidia.com
2. Sign up for free
3. Navigate to **API Keys** or **Console**
4. Create a new API key
5. Copy the key
6. Paste into FreeLLMAPI dashboard under "Nvidia"

**Free Tier Limits:**
- Suitable for production use
- Enterprise-grade reliability

---

### 6. Mistral

**Signup URL:** https://console.mistral.ai

**Available Models:**
- Mistral Large
- Mistral Medium
- Mistral Small
- Codestral (for coding)

**Key Features:**
- Fast and capable models
- Good balance of speed and quality
- Open source alternatives available
- Excellent for code generation

**Setup Steps:**
1. Go to https://console.mistral.ai
2. Sign up for free
3. Navigate to **API Keys**
4. Create a new API key
5. Copy the key
6. Paste into FreeLLMAPI dashboard under "Mistral"

**Free Tier Limits:**
- Good monthly tokens
- Fast response times

---

### 7. OpenRouter

**Signup URL:** https://openrouter.ai

**Available Models:**
- 100+ models from various providers
- GPT-4, Claude, Llama, Mistral, and more
- Curated selection of open source models

**Key Features:**
- Access to massive model selection
- Unified interface for multiple providers
- Pay-as-you-go free tier
- Great for experimenting with different models

**Setup Steps:**
1. Go to https://openrouter.ai
2. Sign up for free
3. Navigate to **API Keys**
4. Create a new API key
5. Copy the key
6. Paste into FreeLLMAPI dashboard under "OpenRouter"

**Free Tier Limits:**
- Limited free tier credits
- Good for testing various models
- Useful as fallback for model variety

---

### 8. Hugging Face

**Signup URL:** https://huggingface.co

**Available Models:**
- Thousands of open source models
- Community-created models
- Fine-tuned versions of popular models

**Key Features:**
- Largest open source model repository
- Community driven
- Free inference API for many models
- Great for experimentation

**Setup Steps:**
1. Go to https://huggingface.co
2. Sign up for free
3. Go to your **Settings** → **Access Tokens**
4. Create a new token
5. Copy the token
6. Paste into FreeLLMAPI dashboard under "Hugging Face"

**Free Tier Limits:**
- Free inference API tier available
- Good for trying community models
- Variable rate limits

---

### 9. Meta (via OpenRouter or Hugging Face)

**Available Models:**
- Llama 3.1 (405B, 70B, 8B)
- Llama 3.0 (various sizes)
- Code Llama

**Key Features:**
- Powerful open source models
- Available through multiple providers
- Great for local and cloud deployment
- Excellent for coding tasks

**How to Access:**
- Through OpenRouter
- Through Hugging Face
- Through other providers that host Llama

---

## Recommended Setup Order

Add providers in this order for optimal performance:

1. **Google AI Studio** (Gemini 2.5)
   - Most capable, primary choice
   - Set as first in fallback chain

2. **Grok** (Groq)
   - Blazing fast, excellent speed
   - Set as second in fallback chain

3. **GitHub Models** (GPT-4o)
   - Premium quality access
   - Set as third in fallback chain

4. **Cerebras**
   - Ultra-fast inference
   - Good fallback option

5. **Mistral**
   - Fast and capable
   - Good general purpose

6. **Others**
   - Add based on your needs
   - OpenRouter for variety
   - Hugging Face for open source

---

## Key Statistics

- **Total Monthly Tokens:** 800+ million combined
- **Number of Providers:** 8+
- **Available Models:** 200+
- **Average Setup Time per Provider:** 2 minutes
- **Cost:** Completely Free

---

## Tips for Maximizing Your Setup

### Add Multiple Providers
The more providers you add, the more resilient your system:
- One provider goes down? Auto-failover to the next
- Hit rate limits? Automatically routes to another
- Different models for different tasks

### Monitor Availability
Use the FreeLLMAPI dashboard to:
- Check which providers are healthy
- View real-time status
- Test models in the playground

### Optimize Your Fallback Chain
- Primary: Capability (Gemini)
- Secondary: Speed (Grok)
- Tertiary: Premium access (GitHub)
- Rest: Redundancy and specialty

### Track Usage
- Use the analytics tab to see which providers you use most
- Understand your usage patterns
- Plan future additions based on needs

---

## Troubleshooting API Keys

### "Unhealthy" Status
- Double-check the API key is copied correctly
- Some keys are very similar—verify character by character
- Check if the API key has expired
- Make sure you're using the right provider name in the dropdown

### Model Not Responding
- Verify the model is available in that provider's free tier
- Check if the provider is currently having issues
- Try a different provider via fallback chain

### Rate Limits Exceeded
- Add more providers to distribute requests
- Reduce request frequency
- Consider which models you're using—some have stricter limits

---

## Future Provider Additions

FreeLLMAPI is actively maintained. New providers may be added including:
- Anthropic Claude (various tiers)
- OpenAI free tier options
- Additional open source providers
- Emerging AI labs

Check the GitHub repository regularly for updates.

---

## Resources

- **FreeLLMAPI GitHub:** https://github.com/freellmapi/freellmapi
- **Official Documentation:** Check repo for latest docs
- **Provider Status:** Monitor your dashboard for real-time status
- **Community:** GitHub issues for questions and discussions

---

**Last Updated:** 2026-06-07  
**Based on:** FreeLLMAPI Tutorial by [Source]
