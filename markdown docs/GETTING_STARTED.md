# FreeLLMAPI - Getting Started Guide

## What is FreeLLMAPI?

FreeLLMAPI is a self-hosted, open-source tool that aggregates free API tiers from major AI providers into one unified endpoint. Instead of managing 14 different accounts and APIs, you get a single OpenAI-compatible interface running on your Windows PC.

### Key Benefits

- **One Unified Endpoint** - Access 14+ AI providers through a single API
- **Free Forever** - Hundreds of millions of tokens every month at no cost
- **Self-Hosted** - Your API keys never leave your machine
- **Automatic Failover** - If one provider goes down, requests automatically route to the next one
- **Beautiful Dashboard** - Manage keys, view analytics, test models, and control failover chains
- **OpenAI Compatible** - Works with LangChain, Llama Index, Open Web UI, and any app using OpenAI's API format

---

## Prerequisites

Before you start, you'll need to install just **two things**:

### 1. Node.js (v20 or higher)
### 2. Git

That's all! Let's get them installed.

---

## Step 1: Install Node.js

1. Open your browser and go to **nodejs.org**
2. Click the big **"Get Node.js"** button
3. Download the **Windows Installer**
4. Double-click the installer and click **Next** through all the prompts
5. Default settings are fine

### Verify Installation

Open Command Prompt and type:
```
node --version
```

You should see something like `v24.something`. If you get an error, close and reopen Command Prompt, then try again.

---

## Step 2: Install Git

1. Go to **git-scm.com**
2. Click **Install for Windows**
3. Download and run the installer
4. Click **Next** through all the prompts
5. Default settings are perfect

### Verify Installation

In Command Prompt, type:
```
git --version
```

You should see something like `Git version 2.something`.

---

## Step 3: Clone the FreeLLMAPI Repository

1. Open Command Prompt or PowerShell
2. Navigate to where you want to store the project (like your C: drive)
3. Run this command:
```
git clone https://github.com/freellmapi/freellmapi.git
```

4. Wait for it to finish downloading the files
5. Navigate into the folder:
```
cd freellmapi
```

---

## Step 4: Install Dependencies

In the freellmapi folder, run:
```
npm install
```

This will download all the packages the project needs. It might take a minute or two, and you'll see lots of text scrolling. This is normal—just let it finish.

### If Installation Fails

If you see errors, try:
```
npm install --force
```

---

## Step 5: Create Environment File (.env)

This file stores your encryption key to keep your API keys safe on disk.

1. In your command prompt, create the .env file:
```
echo. > .env
```

2. Generate and add an encryption key. Copy and paste this command:
```
node -e "require('crypto').randomBytes(32).toString('hex')" | Out-File -Encoding utf8 -Append .env
```

Or if that doesn't work, try:
```
node -e "console.log('ENCRYPTION_KEY=' + require('crypto').randomBytes(32).toString('hex'))" >> .env
```

### Verify It Worked

Type:
```
notepad .env
```

You should see an `ENCRYPTION_KEY` with a long random string. Close Notepad when you're done.

---

## Step 6: Start FreeLLMAPI

Ready for the magic? In PowerShell, run:
```
npm run dev
```

You'll see the terminal spring to life. Within a few seconds, you'll see something like:
```
localhost:5173
```

Click that link (or Ctrl+Click in your terminal) to open the dashboard in your browser.

🎉 **Congratulations!** Your personal AI dashboard is running on your machine with zero monthly fees!

---

## Step 7: Add Your Free API Keys

Now for the fun part. Click on the **Keys** tab in the dashboard.

All of these providers are **completely free to sign up** for:

### Google Gemini (Recommended First)
1. Go to **ai.google.dev**
2. Sign in with your Google account
3. Click **Get API Key** → **Create API Key**
4. Name it `free-llm-api` (optional)
5. Copy the key
6. In the dashboard, select **Google AI Studio** from the dropdown
7. Paste the key and click **Add Key**
8. Done! You now have access to Gemini 2.5 for free

### Grok (For Speed)
1. Go to **console.groq.com**
2. Sign up for free
3. Go to **API Keys**
4. Click **Create API Key**
5. Copy it
6. In the dashboard, select **Grok** from the dropdown
7. Paste the key and click **Add Key**
8. Access to Llama, Mixtral, and other fast models

### GitHub Models (For GPT-4o)
1. Go to **github.com**
2. Click your profile picture → **Settings** → **Developer Settings** → **Personal Access Tokens**
3. Click **Generate New Token**
4. Give it a name and set **No Expiration**
5. Click **Generate**
6. Copy the token
7. In the dashboard, select **GitHub Models**
8. Paste the token and click **Add Key**

### Other Free Providers

The same process applies for all these providers:
- **Cerebras** - cloud.cerebras.ai
- **Nvidia** - build.nvidia.com
- **Mistral** - console.mistral.ai
- **OpenRouter** - openrouter.ai
- **Hugging Face** - huggingface.co

Each takes about 2 minutes to sign up and follows the same pattern: **Sign up** → **Get Key** → **Paste in Dashboard** → **Save**

---

## Step 8: Set Up Your Fallback Chain

The fallback chain tells FreeLLMAPI which provider to try first, second, third, etc.

1. Click on the **Fallback Chain** tab
2. Recommended order:
   - **Gemini 2.5** (most capable free model)
   - **Grok** (fastest inference)
   - **GitHub Models** (access to GPT-4o)
   - Other providers in any order

When one provider is busy or hits rate limits, FreeLLMAPI automatically routes your request to the next one. No configuration needed—it just works!

---

## Step 9: Get Your Unified API Key

1. Click back to the **Keys** tab
2. At the top of the page, you'll see your **Unified Key**
3. Copy this key

This is the **one key** you use for everything. It works with:
- LangChain
- Llama Index
- Open Web UI
- Any app that supports OpenAI's API format

Just change the base URL to `http://localhost:5173/api` and paste your unified key.

---

## Testing Your Setup

### Method 1: Use the Playground

1. Click the **Playground** tab
2. Select a model (or choose **Auto** to let the router decide)
3. Type your message and hit **Send**
4. Watch the response come back with provider information and response time

### Method 2: Use with Your App

Change your OpenAI client configuration:
```
Base URL: http://localhost:5173/api
API Key: [Your Unified Key]
Model: auto (or any specific model name)
```

---

## What You Just Unlocked

By completing this setup, you now have access to:

| Provider | Models | Speed |
|----------|--------|-------|
| **Google** | Gemini 2.5, 1.5 | Very Capable |
| **Grok** | Llama, Mixtral, Grok | Blazing Fast |
| **GitHub** | GPT-4o | Premium Quality |
| **Cerebras** | Llama 3.1 | Very Fast |
| **Nvidia** | Nemotron | Enterprise Ready |
| **Mistral** | Large, Medium | Fast |
| **OpenRouter** | 100+ models | Varied |
| **Hugging Face** | Multiple models | Community |
| ...and more | | |

**Total:** 800+ million tokens per month, completely free.

---

## Troubleshooting

### "Command not found" errors
Make sure you:
- Closed and reopened Command Prompt after installing Node.js and Git
- Are in the correct `freellmapi` folder
- Have completed all prerequisite installations

### npm install fails
Try:
```
npm install --force
```

### .env file issues
Make sure the file has an `ENCRYPTION_KEY` value. If it's empty, delete it and rerun Step 5.

### Dashboard won't load
- Make sure `npm run dev` is still running in your terminal
- Try visiting `http://localhost:5173` directly in your browser
- If still stuck, stop the server (Ctrl+C) and run `npm run dev` again

### API keys show as "unhealthy"
Double-check that you copied the key correctly. Some providers have similar-looking keys—be careful with copy/paste.

---

## Next Steps

1. **Add more API keys** - The more providers you add, the more stable your setup becomes
2. **Experiment with different models** - Try Gemini for capability, Grok for speed
3. **Integrate with your apps** - Use the unified key with LangChain, your custom scripts, etc.
4. **Check analytics** - Visit the **Analytics** tab to see your usage patterns
5. **Explore the playground** - Test different models and prompts before using them in your app

---

## Support & Resources

- **GitHub Repository** - https://github.com/freellmapi/freellmapi
- **Issues & Bugs** - Report on the GitHub repo
- **Contributing** - Pull requests welcome!

---

## Why This is Awesome

✅ **Self-hosted** - Your API keys never leave your machine  
✅ **800M+ tokens/month** - More than most developers will ever use  
✅ **OpenAI compatible** - Drop-in replacement for any OpenAI client  
✅ **Automatic failover** - Never miss a request  
✅ **Beautiful dashboard** - No YAML, no config files, just a clean UI  
✅ **Completely free** - Zero monthly costs

---

**You're all set! Enjoy your personal AI server.** 🚀
