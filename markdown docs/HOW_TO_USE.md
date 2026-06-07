# How to Use FreeLLMAPI

This guide explains how to use FreeLLMAPI with various tools and libraries. FreeLLMAPI provides an **OpenAI-compatible endpoint**, so it works with any tool that supports OpenAI's API format.

---

## Quick Start

**Two things to change in any OpenAI-based code:**

1. **API Key:** Use your FreeLLMAPI unified key (from dashboard)
2. **Base URL:** Use `http://localhost:5173/api`

That's it! Everything else stays the same.

---

## Using with Python OpenAI SDK

### Installation

```bash
pip install openai
```

### Basic Usage

```python
from openai import OpenAI

# Initialize client pointing to FreeLLMAPI
client = OpenAI(
    api_key="your-freellmapi-unified-key",
    base_url="http://localhost:5173/api"
)

# Simple chat completion
response = client.chat.completions.create(
    model="auto",  # Let FreeLLMAPI router decide
    messages=[
        {"role": "user", "content": "What is artificial intelligence?"}
    ]
)

print(response.choices[0].message.content)
```

### Specify a Specific Model

```python
# Use Gemini 2.5
response = client.chat.completions.create(
    model="gemini-2.5-flash",
    messages=[
        {"role": "user", "content": "Explain quantum computing"}
    ]
)
```

### Stream Responses

```python
# Stream the response for real-time output
with client.chat.completions.create(
    model="auto",
    messages=[
        {"role": "user", "content": "Write a short poem about AI"}
    ],
    stream=True
) as stream:
    for text in stream.text_stream:
        print(text, end="", flush=True)
```

### Multi-turn Conversation

```python
messages = []

# User asks a question
messages.append({"role": "user", "content": "What is machine learning?"})

# Get response
response = client.chat.completions.create(
    model="auto",
    messages=messages
)

assistant_response = response.choices[0].message.content
messages.append({"role": "assistant", "content": assistant_response})

# Follow-up question
messages.append({"role": "user", "content": "Can you give me an example?"})

response = client.chat.completions.create(
    model="auto",
    messages=messages
)

print(response.choices[0].message.content)
```

### Using with System Prompts

```python
response = client.chat.completions.create(
    model="auto",
    messages=[
        {
            "role": "system",
            "content": "You are a helpful Python programming assistant."
        },
        {
            "role": "user",
            "content": "How do I read a file in Python?"
        }
    ]
)

print(response.choices[0].message.content)
```

---

## Using with LangChain

### Installation

```bash
pip install langchain langchain-openai
```

### Basic Usage

```python
from langchain_openai import ChatOpenAI

# Initialize LLM with FreeLLMAPI
llm = ChatOpenAI(
    api_key="your-freellmapi-unified-key",
    base_url="http://localhost:5173/api",
    model="auto"
)

# Simple invocation
response = llm.invoke("What is the capital of France?")
print(response.content)
```

### Using with Prompts

```python
from langchain.prompts import ChatPromptTemplate

# Create a prompt template
prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a helpful assistant."),
    ("user", "{input}")
])

# Chain prompt with LLM
chain = prompt | llm

# Invoke chain
response = chain.invoke({"input": "Tell me about renewable energy"})
print(response.content)
```

### Building a RAG Application

```python
from langchain.prompts import ChatPromptTemplate
from langchain.schema.runnable import RunnablePassthrough

# Your custom retriever function
def retrieve_documents(query):
    # Your retrieval logic here
    return "Retrieved context about {query}"

# Create RAG chain
prompt = ChatPromptTemplate.from_template(
    """Based on the following context, answer the question:
    
Context: {context}

Question: {question}

Answer:"""
)

chain = (
    {"context": retrieve_documents, "question": RunnablePassthrough()}
    | prompt
    | llm
)

response = chain.invoke("What are the benefits of solar power?")
print(response.content)
```

### Streaming with LangChain

```python
# Stream responses
for chunk in llm.stream("Write a haiku about nature"):
    print(chunk.content, end="", flush=True)
```

---

## Using with Llama Index

### Installation

```bash
pip install llama-index
```

### Basic Setup

```python
from llama_index.llms.openai import OpenAI
from llama_index.core import Settings

# Configure LLM
llm = OpenAI(
    api_key="your-freellmapi-unified-key",
    base_url="http://localhost:5173/api",
    model="auto"
)

# Set as default LLM
Settings.llm = llm

# Now use in your application
from llama_index.core import Document
from llama_index.core import VectorStoreIndex

documents = [
    Document(text="Your document content here")
]

index = VectorStoreIndex.from_documents(documents)
query_engine = index.as_query_engine()

response = query_engine.query("Your question here?")
print(response)
```

---

## Using with Open Web UI

Open Web UI is a web-based chatbot interface that works with OpenAI-compatible APIs.

### Installation & Setup

1. **Install Docker** (recommended) or install locally
2. **Run Open Web UI:**
   ```bash
   docker run -d -p 3000:8080 --name open-webui ghcr.io/open-webui/open-webui:latest
   ```

3. **Access the interface:**
   - Open `http://localhost:3000` in your browser

4. **Configure FreeLLMAPI:**
   - Click the **Settings** (gear icon)
   - Go to **Connections**
   - Set:
     - **Base URL:** `http://localhost:5173/api`
     - **API Key:** Your FreeLLMAPI unified key
   - Save

5. **Start chatting!**
   - Select your model (or "auto")
   - Start conversations
   - Enjoy the beautiful UI

---

## Using the FreeLLMAPI Dashboard Playground

The fastest way to test FreeLLMAPI without writing code.

### Steps

1. **Open the Dashboard**
   - Visit `http://localhost:5173` in your browser (while `npm run dev` is running)

2. **Click "Playground" Tab**
   - You're now in the testing interface

3. **Select a Model**
   - **"auto"** - Let FreeLLMAPI's router decide
   - **"gemini-2.5-flash"** - Use Gemini
   - **"llama-3.1"** - Use Grok's Llama
   - Any other available model

4. **Type Your Message**
   - Enter your prompt in the input field

5. **Click Send**
   - Watch the response appear

6. **View Details**
   - See which provider served the request
   - Check the response time
   - View token usage

---

## Configuration Reference

### Available Environment Variables

Create a `.env.local` file in your FreeLLMAPI directory:

```env
# Server configuration
PORT=5173
HOST=localhost

# API endpoint
API_BASE_URL=http://localhost:5173/api

# Enable debug logging
DEBUG=true
```

### Available Model Names

Use any of these with the `model` parameter:

**Google:**
- `gemini-2.5-flash`
- `gemini-1.5-pro`

**Grok:**
- `llama-3.1-70b`
- `mixtral-8x7b`
- `grok-2`

**GitHub:**
- `gpt-4o`
- `gpt-4-turbo`

**Cerebras:**
- `llama-3.1-70b`

**Mistral:**
- `mistral-large`
- `mistral-medium`

**Any Model:** Use `auto` to let the router choose

---

## Advanced Usage

### Custom Request Headers

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-key",
    base_url="http://localhost:5173/api",
    default_headers={
        "X-Custom-Header": "value"
    }
)
```

### Handling Errors and Retries

```python
from openai import OpenAI
import time

client = OpenAI(
    api_key="your-key",
    base_url="http://localhost:5173/api",
    max_retries=3  # Auto-retry up to 3 times
)

try:
    response = client.chat.completions.create(
        model="auto",
        messages=[{"role": "user", "content": "Hello"}]
    )
except Exception as e:
    print(f"Error: {e}")
    # FreeLLMAPI will auto-failover to next provider
```

### Monitoring Provider Usage

Check the FreeLLMAPI dashboard **Analytics** tab to see:
- Which providers you're using most
- Token consumption per provider
- Request counts
- Response times

---

## Use Cases & Examples

### Example 1: Content Generation

```python
from openai import OpenAI

client = OpenAI(
    api_key="your-key",
    base_url="http://localhost:5173/api"
)

prompt = """Generate 5 creative blog post titles about sustainable living."""

response = client.chat.completions.create(
    model="gemini-2.5-flash",  # Best for generation tasks
    messages=[{"role": "user", "content": prompt}]
)

print(response.choices[0].message.content)
```

### Example 2: Code Generation (Use Grok for Speed)

```python
response = client.chat.completions.create(
    model="llama-3.1-70b",  # Via Grok (fast)
    messages=[{
        "role": "user",
        "content": "Write a Python function to calculate fibonacci numbers"
    }]
)
```

### Example 3: Analysis & Summarization

```python
response = client.chat.completions.create(
    model="auto",  # Let router pick
    messages=[{
        "role": "user",
        "content": f"""Summarize the following text in 3 sentences:
        
{long_text_to_summarize}"""
    }]
)
```

### Example 4: Chatbot with Context

```python
conversation_history = []

def chat(user_message):
    conversation_history.append({
        "role": "user",
        "content": user_message
    })
    
    response = client.chat.completions.create(
        model="auto",
        messages=conversation_history
    )
    
    assistant_message = response.choices[0].message.content
    conversation_history.append({
        "role": "assistant",
        "content": assistant_message
    })
    
    return assistant_message

# Use it
print(chat("What's the weather?"))
print(chat("Should I bring an umbrella?"))  # Context aware!
```

---

## Troubleshooting

### "Connection refused" Error

**Problem:** Can't connect to `localhost:5173`

**Solution:**
- Make sure `npm run dev` is running in a terminal
- Check that FreeLLMAPI is fully started
- Try accessing `http://localhost:5173` in a browser

### "Invalid API key" Error

**Problem:** API key not recognized

**Solution:**
- Copy your unified key from the FreeLLMAPI dashboard **Keys** tab
- Make sure you copied the entire key
- Verify no spaces or extra characters

### "Model not found" Error

**Problem:** The model name isn't recognized

**Solution:**
- Use `auto` if unsure
- Check available models in the dashboard
- Verify the provider for that model is enabled

### Slow Responses

**Problem:** Responses are taking too long

**Solution:**
- Try using `llama-3.1-70b` or `mixtral-8x7b` via Grok (fastest)
- Check the **Analytics** tab to see current provider health
- Increase your fallback chain providers

---

## Performance Tips

1. **Use `auto` for best performance**
   - Router picks the fastest available provider
   - Automatic failover if one is busy

2. **Use Grok for speed-critical tasks**
   - Fastest inference available
   - Great for real-time applications

3. **Use Gemini for complex reasoning**
   - Most capable model
   - Better for complex tasks

4. **Monitor your usage**
   - Check the Analytics dashboard regularly
   - Understand which providers you use most

5. **Add multiple providers**
   - More redundancy
   - Better fallover coverage

---

## Complete Working Example

```python
from openai import OpenAI

# Initialize
client = OpenAI(
    api_key="your-freellmapi-unified-key",
    base_url="http://localhost:5173/api"
)

# Start conversation
def main():
    messages = []
    print("Chat with FreeLLMAPI (type 'quit' to exit)\n")
    
    while True:
        user_input = input("You: ").strip()
        
        if user_input.lower() == "quit":
            break
        
        messages.append({"role": "user", "content": user_input})
        
        response = client.chat.completions.create(
            model="auto",
            messages=messages
        )
        
        assistant_response = response.choices[0].message.content
        messages.append({"role": "assistant", "content": assistant_response})
        
        print(f"Assistant: {assistant_response}\n")

if __name__ == "__main__":
    main()
```

---

## Resources

- **Official Docs:** Check FreeLLMAPI GitHub
- **Dashboard:** http://localhost:5173 (while running)
- **OpenAI SDK Docs:** https://platform.openai.com/docs
- **LangChain Docs:** https://python.langchain.com
- **Llama Index Docs:** https://docs.llamaindex.ai

---

**Remember:** FreeLLMAPI is OpenAI-compatible, so any tool that works with OpenAI will work with FreeLLMAPI. Just change the endpoint URL!
