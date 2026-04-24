# LangChain for Beginners: Building AI Apps with Python

## What is LangChain?

Imagine you want to build a smart chatbot or an app that can answer questions about your documents. Normally, you'd have to write a lot of code to connect to AI models, handle conversations, and manage data. LangChain is like a LEGO set that gives you pre-made pieces to build these AI apps quickly.

**Key idea**: LangChain helps you connect AI language models to your data, tools, and logic without reinventing the wheel.

---

## Table of Contents

1. [Getting Started: Installation](#getting-started-installation)
2. [Your First LangChain App](#your-first-langchain-app)
3. [Core Building Blocks](#core-building-blocks)
   - [AI Models (LLMs and Chat)](#ai-models-llms-and-chat)
   - [Prompts: Talking to AI](#prompts-talking-to-ai)
   - [Chains: Linking Steps Together](#chains-linking-steps-together)
   - [Agents: Smart Decision Makers](#agents-smart-decision-makers)
   - [Memory: Remembering Conversations](#memory-remembering-conversations)
   - [Search and Retrieval: Finding Information](#search-and-retrieval-finding-information)
4. [Working with Different AI Models](#working-with-different-ai-models)
5. [Advanced Features](#advanced-features)
6. [Real-World Examples](#real-world-examples)
7. [Making Your App Production-Ready](#making-your-app-production-ready)
8. [Safety and Best Practices](#safety-and-best-practices)
9. [When Things Go Wrong](#when-things-go-wrong)
10. [Where to Learn More](#where-to-learn-more)

---

## Getting Started: Installation

1. Install Python 3.8+.
2. Run `pip install langchain pgvector`.
3. Set up PostgreSQL with pgvector extension (see https://github.com/pgvector/pgvector).
4. Add `OPENAI_API_KEY=your_actual_key_here` to `.env`.
5. Verify with:

```python
import langchain
print(langchain.__version__)
```

---

## Your First LangChain App

Let's build something simple to see how it works.

```python
import os
from langchain.llms import OpenAI

# Load your API key
os.environ["OPENAI_API_KEY"] = "your-key-here"

# Connect to the AI
llm = OpenAI(temperature=0.7)  # temperature controls creativity (0-1)

# Ask a question
response = llm("What is the capital of France?")
print(response)  # Should print "Paris"
```

---

## Core Building Blocks

LangChain has 6 main concepts that you combine like building blocks. Think of them as ingredients in a recipe.

### AI Models (LLMs and Chat)

These are the "brains" of your app. There are two main types:

#### Text Completion Models (LLMs)
Good for single questions or generating text.

```python
from langchain.llms import OpenAI

llm = OpenAI()
story = llm("Write a short story about a robot")
print(story)
```

#### Chat Models
Better for conversations, like talking to a person.

```python
from langchain.chat_models import ChatOpenAI
from langchain.schema import HumanMessage, SystemMessage

chat = ChatOpenAI()
messages = [
    SystemMessage(content="You are a helpful teacher."),
    HumanMessage(content="Explain gravity simply.")
]
response = chat(messages)
print(response.content)
```

**Analogy**: LLMs are like writing an email. Chat models are like having a conversation.

### Prompts: Talking to AI

Prompts are instructions you give to the AI. Good prompts = good answers.

#### Simple Prompts
```python
from langchain.prompts import PromptTemplate

template = PromptTemplate(
    input_variables=["topic"],
    template="Explain {topic} like I'm 5 years old."
)

prompt = template.format(topic="the internet")
print(prompt)  # "Explain the internet like I'm 5 years old."
```

#### Chat Prompts
For conversations with roles.

```python
from langchain.prompts import ChatPromptTemplate

chat_template = ChatPromptTemplate.from_messages([
    ("system", "You are a {role} assistant."),
    ("human", "Tell me about {topic}.")
])

messages = chat_template.format_messages(
    role="friendly",
    topic="pizza"
)
```

**Why important?** AI needs clear instructions to give good answers.

### Chains: Linking Steps Together

Chains connect multiple steps. Like a recipe: mix ingredients → bake → cool.

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

# Step 1: Create prompt
prompt = PromptTemplate(
    input_variables=["topic"],
    template="Write a poem about {topic}."
)

# Step 2: Create chain
chain = LLMChain(llm=llm, prompt=prompt)

# Step 3: Run it
poem = chain.run(topic="sunsets")
print(poem)
```

**Advanced chains:**
- Sequential: Step 1 → Step 2 → Step 3
- Router: Choose different paths based on input
- Custom: Build your own logic

### Agents: Smart Decision Makers

Agents can think and choose what to do. They use "tools" to help.

```python
from langchain.agents import initialize_agent
from langchain.tools import tool

@tool
def multiply(a: int, b: int) -> int:
    """Multiply two numbers."""
    return a * b

# Create agent with calculator tool
agent = initialize_agent([multiply], llm, agent="zero-shot-react-description")

# Agent can now do math!
result = agent.run("What is 15 times 7?")
print(result)  # Should calculate and answer

# OR

@tool
def get_weather(city: str) -> str:
    """Get weather for a city."""
    response = requests.get(f"https://api.weather.com/{city}")
    return response.json()
# Now the Agent can get Weather live update.

# OR 

@tool
def check_order(order_id: str) -> str:
    """Check order status."""
    # Connect to your order database
    return f"Order {order_id} is shipped."

tools = [check_order]
agent = initialize_agent(tools, llm, agent="conversational-react-description")

response = agent.run("Where is my order #12345?")
```

**Tools agents can use:**
- Search the web
- Check databases
- Send emails
- Run code
- Use APIs

### Memory: Remembering Conversations

Without memory, AI forgets everything after each message.

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

memory = ConversationBufferMemory()
conversation = ConversationChain(llm=llm, memory=memory)

conversation.predict(input="Hi, I'm Alice.")
conversation.predict(input="What's my name?")
# AI remembers: "Your name is Alice."
```

**Memory types:**
- Buffer: Keep all messages
- Window: Keep recent messages only
- Summary: Summarize old conversations

### Search and Retrieval: Finding Information

Help your app search through documents intelligently.

```python
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings

# 1. Prepare documents
documents = ["AI is changing the world.", "Python is a programming language."]

# 2. Create searchable index
embeddings = OpenAIEmbeddings()
connection_string = "postgresql://user:password@localhost:5432/dbname"  # Replace with your PostgreSQL connection
vectorstore = PGVector.from_texts(documents, embeddings, connection_string=connection_string, collection_name="my_docs")

# 3. Search
results = vectorstore.similarity_search("What is programming?")
print(results)  # Finds relevant documents
```

### **RAG (Retrieval-Augmented Generation):**
Retrieval-Augmented Generation (RAG) is a powerful technique that combines the strengths of retrieval-based systems and generative AI. Instead of relying solely on what the AI model "remembers" from its training data, RAG retrieves relevant information from your own documents or knowledge base to provide more accurate, up-to-date, and factual answers.

**How RAG works:**
1. **Index your documents**: Convert your documents into searchable vectors using embeddings
2. **User asks a question**: The system receives a query
3. **Retrieve relevant info**: Search the vector store for the most relevant document chunks
4. **Generate answer**: Feed the retrieved information + the question to the AI model
5. **Get factual response**: The AI generates an answer grounded in your actual data

**Benefits of RAG:**
- **Reduces hallucinations**: Answers are based on real data, not just model training
- **Stays current**: Can incorporate new information without retraining the model
- **Cost-effective**: No need for expensive fine-tuning for domain-specific knowledge
- **Transparent**: You can see the source documents used for the answer

**Simple RAG example:**
```python
from langchain.chains import RetrievalQA

# Create a retriever from your vector store
retriever = vectorstore.as_retriever(search_kwargs={"k": 3})

# Build RAG chain
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=retriever,
    chain_type="stuff"  # Combines retrieved docs into context
)

# Ask questions grounded in your documents
answer = qa_chain.run("What does your company policy say about remote work?")
print(answer)
```

---

## Working with Different AI Models

LangChain works with many AI providers. You can switch easily!

### Popular Options

```python
# OpenAI (most common)
from langchain.llms import OpenAI
llm = OpenAI()

# Anthropic (Claude)
from langchain.llms import Anthropic
llm = Anthropic()

# Hugging Face (free models)
from langchain.llms import HuggingFaceHub
llm = HuggingFaceHub(repo_id="google/flan-t5-base")
```

### Model Settings

```python
llm = OpenAI(
    temperature=0.1,    # Low = consistent, High = creative
    max_tokens=100,     # Max response length
    model_name="gpt-4"  # Which model to use
)
```

---

## Advanced Features

### Document Processing

Load and process different file types:

```python
from langchain.document_loaders import TextLoader, PyPDFLoader

# Load text file
loader = TextLoader("my_document.txt")
documents = loader.load()

# Load PDF
loader = PyPDFLoader("document.pdf")
documents = loader.load()
```

### Database Connections

Connect to databases:

```python
from langchain.utilities import SQLDatabase

db = SQLDatabase.from_uri("postgresql://user:password@localhost:5432/mydb")
# Now you can query your database with AI
```

### API Integrations

Connect to web services:

```python
from langchain.tools import tool
import requests

@tool
def get_weather(city: str) -> str:
    """Get weather for a city."""
    response = requests.get(f"https://api.weather.com/{city}")
    return response.json()

# Agent can now check weather!
```

### Streaming and Async

Get responses as they're generated (faster feel):

```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

llm = OpenAI(callbacks=[StreamingStdOutCallbackHandler()])
# Response appears character by character
```

---

## Real-World Examples

### Chatbot for Customer Support

```python
from langchain.agents import initialize_agent
from langchain.tools import tool

@tool
def check_order(order_id: str) -> str:
    """Check order status."""
    # Connect to your order database
    return f"Order {order_id} is shipped."

tools = [check_order]
agent = initialize_agent(tools, llm, agent="conversational-react-description")

response = agent.run("Where is my order #12345?")
```

### Document Q&A System

```python
from langchain.chains import RetrievalQA

# Load your documents
vectorstore = PGVector.from_texts(your_documents, embeddings, connection_string=connection_string, collection_name="manual")
retriever = vectorstore.as_retriever()

# Create Q&A chain
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    retriever=retriever
)

answer = qa_chain.run("What does the manual say about troubleshooting?")
```

### Content Generator

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

template = PromptTemplate(
    input_variables=["topic", "audience"],
    template="""Write a {audience}-friendly article about {topic}.
    Include a catchy title and 3 main points."""
)

chain = LLMChain(llm=llm, prompt=template)
article = chain.run(topic="AI in healthcare", audience="beginner")
```

---

## Making Your App Production-Ready

### Containerization with Docker

Package your app so it runs anywhere:

```dockerfile
FROM python:3.9
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

### Error Handling

```python
from tenacity import retry, stop_after_attempt

@retry(stop=stop_after_attempt(3))
def call_ai(prompt):
    try:
        return llm(prompt)
    except Exception as e:
        print(f"Error: {e}")
        raise
```

### Monitoring

```python
from langchain.callbacks import get_callback_manager

# Track usage and performance
callback_manager = get_callback_manager()
llm = OpenAI(callback_manager=callback_manager)
```

---

## Safety and Best Practices

### Input Sanitization

Clean user inputs to prevent problems:

```python
import re

def clean_input(text: str) -> str:
    # Remove dangerous characters
    return re.sub(r'[^\w\s]', '', text)
```

### Rate Limiting

Don't overwhelm AI services:

```python
import time

def rate_limited_call(prompt):
    time.sleep(1)  # Wait 1 second between calls
    return llm(prompt)
```

### Secure API Keys

Never put keys in code:

```python
# Good: Use environment variables
import os
api_key = os.environ["OPENAI_API_KEY"]

# Bad: Hardcode keys
api_key = "sk-1234567890abcdef"
```

### Privacy Considerations

- Don't store sensitive user data
- Be clear about data usage
- Follow privacy laws (GDPR, etc.)

---

## When Things Go Wrong

### Common Problems

#### API Key Issues
```python
# Check if key exists
import os
if "OPENAI_API_KEY" not in os.environ:
    print("API key missing!")

# Check key format
key = os.environ.get("OPENAI_API_KEY", "")
if not key.startswith("sk-"):
    print("Invalid key format")
```

#### Rate Limits
AI services limit how many requests you can make.

```python
from tenacity import retry, wait_exponential

@retry(wait=wait_exponential(multiplier=1, max=60))
def safe_call(prompt):
    return llm(prompt)
```

#### Memory Issues
For long conversations:

```python
# Use windowed memory
from langchain.memory import ConversationBufferWindowMemory
memory = ConversationBufferWindowMemory(k=5)  # Keep last 5 exchanges
```

#### Import Errors
Missing packages:

```bash
pip install langchain[all]  # Install everything
```

### Debugging Tips

```python
# Enable detailed logging
import logging
logging.basicConfig(level=logging.DEBUG)

# Make chains verbose
chain = LLMChain(llm=llm, prompt=prompt, verbose=True)
```

---

## Where to Learn More

### Official Resources
- [LangChain Documentation](https://python.langchain.com/)
- [LangChain GitHub](https://github.com/langchain-ai/langchain)

### Learning Paths
- Start with basic examples
- Try modifying code
- Build small projects
- Join the community

### Community
- [LangChain Discord](https://discord.gg/langchain)
- [Stack Overflow](https://stackoverflow.com/questions/tagged/langchain)

### Courses
- [DeepLearning.AI LangChain Course](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/)

---

## Final Tips for Beginners

1. **Start Small**: Begin with simple examples, not complex apps
2. **Experiment**: Change parameters and see what happens
3. **Read Error Messages**: They tell you what's wrong
4. **Use the Docs**: LangChain has great documentation
5. **Join Community**: Ask questions and learn from others
6. **Practice**: Build something every day

Remember: Everyone starts as a beginner. The key is persistence and curiosity. You can build amazing AI apps with LangChain!

Happy coding! 🚀

template = PromptTemplate(
    input_variables=["topic"],
    template="Write a short summary about {topic}."
)

prompt = template.format(topic="artificial intelligence")
print(prompt)
```

#### Chat Prompt Templates

Chat prompt templates let you build prompt structures for chat-based models. They combine system instructions, user queries, and optional example messages into a format that chat models can interpret reliably.

```python
from langchain.prompts import ChatPromptTemplate, HumanMessagePromptTemplate, SystemMessagePromptTemplate

system_template = "You are a {role} assistant."
human_template = "Explain {concept} in simple terms."

chat_prompt = ChatPromptTemplate.from_messages([
    SystemMessagePromptTemplate.from_template(system_template),
    HumanMessagePromptTemplate.from_template(human_template)
])

messages = chat_prompt.format_messages(role="helpful", concept="machine learning")
```

### Chains

Chains are workflows that connect multiple LangChain components together. A chain can take inputs, run them through prompts, call LLMs, process outputs, and pass results to the next step. This makes it easy to build multi-stage pipelines and reusable application logic.

#### Simple Chain Example

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["topic"],
    template="Explain {topic} in one sentence."
)

chain = LLMChain(llm=llm, prompt=prompt)
result = chain.run(topic="quantum computing")
print(result)
```

### Agents

Agents extend the chain concept with decision making. They can choose between tools, execute actions, and respond dynamically based on the input and tool results. Agents are ideal for tasks that require reasoning, external data lookup, or multi-step problem solving.

#### Basic Agent Example

```python
from langchain.agents import initialize_agent, Tool
from langchain.tools import tool

@tool
def multiply(a: int, b: int) -> int:
    """Multiply two numbers."""
    return a * b

tools = [multiply]
agent = initialize_agent(tools, llm, agent="zero-shot-react-description")
result = agent.run("What is 15 times 4?")
print(result)
```

### Memory

Memory is the mechanism that helps LangChain remember information across interactions. It can store conversation history, summarize earlier turns, track entities, and inject relevant context into future prompts.

#### Conversation Buffer Memory

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

memory = ConversationBufferMemory()
conversation = ConversationChain(
    llm=llm,
    memory=memory,
    verbose=True
)

conversation.predict(input="Hi, my name is Alice.")
conversation.predict(input="What's my name?")
```

### Indexes and Retrievers

Indexes and retrievers power retrieval-augmented generation (RAG). LangChain builds searchable indexes over documents using vector embeddings. A retriever finds the most relevant documents for a query, and those documents can then be added to an LLM prompt to provide grounded, factual answers.

#### Basic Retriever Example

```python
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings
from langchain.text_splitter import CharacterTextSplitter

# Split documents
text_splitter = CharacterTextSplitter(chunk_size=1000, chunk_overlap=0)
texts = text_splitter.split_documents(documents)

# Create embeddings and store
embeddings = OpenAIEmbeddings()
connection_string = "postgresql://user:password@localhost:5432/dbname"
vectorstore = PGVector.from_documents(texts, embeddings, connection_string=connection_string, collection_name="docs")

# Create retriever
retriever = vectorstore.as_retriever()
```

---

## Getting Started

Let's create a simple LangChain application.

```python
import os
from langchain.llms import OpenAI
from langchain.prompts import PromptTemplate
from langchain.chains import LLMChain

# Set up API key
os.environ["OPENAI_API_KEY"] = "your-api-key-here"

# Initialize LLM
llm = OpenAI(temperature=0.7)

# Create prompt template
prompt = PromptTemplate(
    input_variables=["topic"],
    template="Write a creative story about {topic}."
)

# Create chain
chain = LLMChain(llm=llm, prompt=prompt)

# Run the chain
story = chain.run(topic="a robot learning to paint")
print(story)
```

---

## Working with LLMs

Working with LLMs means selecting the right model and configuring it for your task. LangChain supports many providers and makes it easy to swap models or adjust parameters like temperature, max tokens, and streaming.

### Supported LLM Providers

LangChain supports numerous LLM providers:

- OpenAI (GPT-3.5, GPT-4)
- Anthropic (Claude)
- Hugging Face
- Cohere
- AI21 Labs
- Replicate
- Together AI
- And many more

### Configuring LLMs

```python
from langchain.llms import OpenAI

# Basic configuration
llm = OpenAI(
    model_name="gpt-3.5-turbo",
    temperature=0.7,
    max_tokens=150,
    top_p=1,
    frequency_penalty=0,
    presence_penalty=0
)

# Advanced configuration
llm = OpenAI(
    model_name="gpt-4",
    temperature=0.1,
    max_tokens=500,
    stop=["\n"],
    n=1,
    best_of=None,
    logit_bias=None
)
```

### Streaming Responses

```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

llm = OpenAI(
    streaming=True,
    callbacks=[StreamingStdOutCallbackHandler()]
)

response = llm("Write a haiku about programming.")
```

### Async Operations

```python
import asyncio
from langchain.llms import OpenAI

llm = OpenAI()

async def generate_text():
    response = await llm.agenerate(["Tell me a joke."])
    print(response.generations[0][0].text)

asyncio.run(generate_text())
```

---

## Prompt Engineering

Prompt engineering is the practice of designing high-quality instructions for language models. LangChain provides tools to create reusable templates, few-shot examples, and structured chat prompts so your prompts are consistent and maintainable.

### Basic Prompt Templates

```python
from langchain.prompts import PromptTemplate

# Simple template
template = PromptTemplate(
    input_variables=["product"],
    template="What are the benefits of using {product}?"
)

# Template with multiple variables
template = PromptTemplate(
    input_variables=["topic", "style"],
    template="Explain {topic} in a {style} way."
)

# Template with partial variables
template = PromptTemplate(
    input_variables=["topic"],
    partial_variables={"style": "simple"},
    template="Explain {topic} in a {style} way."
)
```

### Few-Shot Prompting

```python
from langchain.prompts import FewShotPromptTemplate

examples = [
    {"input": "happy", "output": "sad"},
    {"input": "tall", "output": "short"},
    {"input": "hot", "output": "cold"}
]

example_prompt = PromptTemplate(
    input_variables=["input", "output"],
    template="Input: {input}\nOutput: {output}"
)

prompt = FewShotPromptTemplate(
    examples=examples,
    example_prompt=example_prompt,
    prefix="Find the antonym of the word:",
    suffix="Input: {word}\nOutput:",
    input_variables=["word"]
)

print(prompt.format(word="big"))
```

### Chat Prompt Templates

```python
from langchain.prompts import ChatPromptTemplate, HumanMessagePromptTemplate, AIMessagePromptTemplate, SystemMessagePromptTemplate

template = ChatPromptTemplate.from_messages([
    SystemMessagePromptTemplate.from_template(
        "You are a {role} assistant. Answer in {language}."
    ),
    HumanMessagePromptTemplate.from_template("{question}"),
    AIMessagePromptTemplate.from_template("First, I need to understand the question..."),
    HumanMessagePromptTemplate.from_template("Please provide a detailed answer.")
])

messages = template.format_messages(
    role="helpful",
    language="English",
    question="What is machine learning?"
)
```

### Prompt Validation

```python
from langchain.prompts import PromptTemplate
from pydantic import BaseModel, validator

class ValidatedPromptTemplate(PromptTemplate):
    @validator("template")
    def validate_template(cls, v):
        if len(v) < 10:
            raise ValueError("Template must be at least 10 characters long")
        return v
```

---

## Chains in Depth

This section dives deeper into chain types and workflows. LangChain provides several chain abstractions for sequential processing, branching, routing, and custom transformation logic.

### LLMChain

The most basic chain type, used for single prompt-to-LLM workflows.

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

prompt = PromptTemplate(
    input_variables=["topic", "level"],
    template="Explain {topic} at a {level} level."
)

chain = LLMChain(
    llm=llm,
    prompt=prompt,
    verbose=True,
    output_key="explanation"
)

result = chain({
    "topic": "quantum physics",
    "level": "beginner"
})

print(result["explanation"])
```

### Sequential Chains

Combine multiple chains in sequence.

```python
from langchain.chains import SequentialChain, LLMChain
from langchain.prompts import PromptTemplate

# First chain: Generate topic
topic_prompt = PromptTemplate(
    input_variables=["subject"],
    template="Generate an interesting topic related to {subject}."
)

topic_chain = LLMChain(
    llm=llm,
    prompt=topic_prompt,
    output_key="topic"
)

# Second chain: Write article
article_prompt = PromptTemplate(
    input_variables=["topic"],
    template="Write a 200-word article about {topic}."
)

article_chain = LLMChain(
    llm=llm,
    prompt=article_prompt,
    output_key="article"
)

# Combine chains
overall_chain = SequentialChain(
    chains=[topic_chain, article_chain],
    input_variables=["subject"],
    output_variables=["topic", "article"],
    verbose=True
)

result = overall_chain({"subject": "artificial intelligence"})
print(f"Topic: {result['topic']}")
print(f"Article: {result['article']}")
```

### Custom Chains

Create your own chain classes.

```python
from langchain.chains.base import Chain
from langchain.schema import BaseLanguageModel
from typing import Dict, List, Any

class CustomChain(Chain):
    llm: BaseLanguageModel
    custom_param: str = "default"
    
    @property
    def input_keys(self) -> List[str]:
        return ["input_text"]
    
    @property
    def output_keys(self) -> List[str]:
        return ["output_text", "metadata"]
    
    def _call(self, inputs: Dict[str, Any]) -> Dict[str, Any]:
        # Custom logic here
        text = inputs["input_text"]
        processed = self.llm(f"Process this text: {text}")
        
        return {
            "output_text": processed,
            "metadata": {"length": len(text), "param": self.custom_param}
        }
```

### Router Chains

Route inputs to different chains based on conditions.

```python
from langchain.chains.router import MultiPromptChain
from langchain.chains.router.llm_router import LLMRouterChain, RouterOutputParser
from langchain.prompts import PromptTemplate

# Define destination chains
physics_template = """You are a physics expert. Answer the question: {input}"""
math_template = """You are a math expert. Answer the question: {input}"""

prompt_infos = [
    {
        "name": "physics",
        "description": "Good for answering questions about physics",
        "prompt_template": physics_template
    },
    {
        "name": "math", 
        "description": "Good for answering questions about math",
        "prompt_template": math_template
    }
]

# Create router
router_template = """Given a question, decide which subject it belongs to.

Question: {input}

Return only the name of the subject: physics or math."""

router_prompt = PromptTemplate(
    template=router_template,
    input_variables=["input"],
    output_parser=RouterOutputParser()
)

router_chain = LLMRouterChain.from_llm(llm, router_prompt)

# Create destination chains
destination_chains = {}
for p_info in prompt_infos:
    name = p_info["name"]
    prompt_template = p_info["prompt_template"]
    prompt = PromptTemplate(template=prompt_template, input_variables=["input"])
    chain = LLMChain(llm=llm, prompt=prompt)
    destination_chains[name] = chain

# Default chain for unmatched inputs
default_prompt = PromptTemplate(
    template="Answer the following question: {input}",
    input_variables=["input"]
)
default_chain = LLMChain(llm=llm, prompt=default_prompt)

chain = MultiPromptChain(
    router_chain=router_chain,
    destination_chains=destination_chains,
    default_chain=default_chain,
    verbose=True
)
```

### Transformation Chains

Transform inputs before passing to LLMs.

```python
from langchain.chains import TransformChain, LLMChain
from langchain.prompts import PromptTemplate

def transform_func(inputs: dict) -> dict:
    """Transform the input text."""
    text = inputs["text"]
    # Transform logic here
    transformed = text.upper()
    return {"transformed_text": transformed}

transform_chain = TransformChain(
    input_variables=["text"],
    output_variables=["transformed_text"],
    transform=transform_func
)

# Combine with LLM chain
llm_prompt = PromptTemplate(
    input_variables=["transformed_text"],
    template="Summarize: {transformed_text}"
)

llm_chain = LLMChain(llm=llm, prompt=llm_prompt)

# Sequential execution
from langchain.chains import SimpleSequentialChain
overall_chain = SimpleSequentialChain(
    chains=[transform_chain, llm_chain],
    verbose=True
)

result = overall_chain.run("hello world")
```

### Chain Composition Patterns

#### Pipeline Pattern

```python
from langchain.chains import LLMChain, TransformChain
from langchain.prompts import PromptTemplate

# Data preprocessing
def preprocess_data(inputs):
    text = inputs["raw_text"]
    # Preprocessing logic
    cleaned = text.strip().lower()
    return {"processed_text": cleaned}

preprocess_chain = TransformChain(
    input_variables=["raw_text"],
    output_variables=["processed_text"],
    transform=preprocess_data
)

# Feature extraction
extract_prompt = PromptTemplate(
    input_variables=["processed_text"],
    template="Extract key features from: {processed_text}"
)

extract_chain = LLMChain(llm=llm, prompt=extract_prompt)

# Analysis
analyze_prompt = PromptTemplate(
    input_variables=["features"],
    template="Analyze these features: {features}"
)

analyze_chain = LLMChain(llm=llm, prompt=analyze_prompt)

# Pipeline
from langchain.chains import SequentialChain
pipeline = SequentialChain(
    chains=[preprocess_chain, extract_chain, analyze_chain],
    input_variables=["raw_text"],
    output_variables=["analysis"],
    verbose=True
)
```

#### Fan-out/Fan-in Pattern

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

# Multiple parallel analyses
analysis_prompts = [
    PromptTemplate(input_variables=["text"], template="Analyze sentiment: {text}"),
    PromptTemplate(input_variables=["text"], template="Extract entities: {text}"),
    PromptTemplate(input_variables=["text"], template="Summarize content: {text}")
]

analysis_chains = [
    LLMChain(llm=llm, prompt=prompt) for prompt in analysis_prompts
]

# Aggregation chain
aggregate_prompt = PromptTemplate(
    input_variables=["sentiment", "entities", "summary"],
    template="""Combine these analyses:
    Sentiment: {sentiment}
    Entities: {entities}
    Summary: {summary}
    
    Provide a final assessment:"""
)

aggregate_chain = LLMChain(llm=llm, prompt=aggregate_prompt)

# Note: LangChain doesn't have built-in fan-out/fan-in, but you can implement it
```

#### Conditional Branching

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

def route_based_on_complexity(inputs):
    text = inputs["text"]
    # Simple complexity check
    if len(text.split()) > 50:
        return "complex_analysis"
    else:
        return "simple_summary"

# Different chains for different complexity levels
simple_prompt = PromptTemplate(
    input_variables=["text"],
    template="Provide a brief summary: {text}"
)

complex_prompt = PromptTemplate(
    input_variables=["text"],
    template="Provide a detailed analysis with key points and implications: {text}"
)

simple_chain = LLMChain(llm=llm, prompt=simple_prompt)
complex_chain = LLMChain(llm=llm, prompt=complex_prompt)

# Custom routing chain
class ConditionalChain(Chain):
    router_function: callable
    chains: dict
    
    def _call(self, inputs):
        route = self.router_function(inputs)
        return self.chains[route](inputs)
```

---

## Agents and Tools

Agents are higher-level controllers that can call tools and make decisions based on model outputs. Tools are functions or utilities exposed to agents, enabling them to interact with external systems, perform calculations, fetch data, or manipulate content. Together, agents and tools let LangChain perform complex, multi-step tasks.

### Built-in Agents

LangChain provides several pre-built agent types.

#### Zero-Shot ReAct Agent

```python
from langchain.agents import initialize_agent, AgentType
from langchain.tools import tool

@tool
def calculator(expression: str) -> str:
    """Evaluate a mathematical expression."""
    try:
        return str(eval(expression))
    except:
        return "Invalid expression"

tools = [calculator]

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)

result = agent.run("What is 15 * 7 + 3?")
print(result)
```

#### Conversational Agent

```python
from langchain.agents import initialize_agent
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory(memory_key="chat_history")

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.CONVERSATIONAL_REACT_DESCRIPTION,
    memory=memory,
    verbose=True
)

agent.run("Hi, I'm Alice.")
agent.run("What's my name?")
```

#### Structured Chat Agent

```python
from langchain.agents import initialize_agent
from langchain.agents.agent_types import AgentType

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.STRUCTURED_CHAT_ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)
```

### Custom Agents

Create agents with custom logic.

```python
from langchain.agents import Agent
from langchain.schema import AgentAction, AgentFinish
from typing import List, Tuple, Any, Union

class CustomAgent(Agent):
    @property
    def input_keys(self):
        return ["input"]
    
    def plan(self, intermediate_steps: List[Tuple[AgentAction, str]], **kwargs) -> Union[AgentAction, AgentFinish]:
        # Custom planning logic
        input_text = kwargs["input"]
        
        if "calculate" in input_text.lower():
            return AgentAction(tool="calculator", tool_input=input_text, log="Using calculator")
        else:
            return AgentFinish(
                return_values={"output": f"I don't know how to handle: {input_text}"},
                log="No appropriate tool found"
            )
```

### Tools

Tools are functions that agents can use.

#### Built-in Tools

```python
from langchain.tools import DuckDuckGoSearchRun, WikipediaQueryRun, WolframAlphaQueryRun

search = DuckDuckGoSearchRun()
wikipedia = WikipediaQueryRun()
wolfram = WolframAlphaQueryRun()

tools = [search, wikipedia, wolfram]
```

#### Custom Tools

```python
from langchain.tools import BaseTool
from typing import Optional

class CustomTool(BaseTool):
    name = "custom_tool"
    description = "A custom tool for demonstration"
    
    def _run(self, query: str) -> str:
        # Tool logic here
        return f"Processed: {query}"
    
    async def _arun(self, query: str) -> str:
        # Async version
        return f"Async processed: {query}"
```

#### Toolkits

Group related tools together.

```python
from langchain.agents import load_tools

# Load a toolkit
tools = load_tools(["serpapi", "llm-math"], llm=llm)

# Or create custom toolkit
from langchain.tools import Tool
from langchain.utilities import GoogleSearchAPIWrapper

search = GoogleSearchAPIWrapper()
tools = [
    Tool(
        name="Google Search",
        func=search.run,
        description="Search Google for information"
    )
]
```

### Agent Executors

Control agent execution with custom logic.

```python
from langchain.agents import AgentExecutor
from langchain.agents import initialize_agent

agent = initialize_agent(tools, llm, agent="zero-shot-react-description")

# Custom executor with additional logic
class CustomAgentExecutor(AgentExecutor):
    def _call(self, inputs, run_manager=None):
        # Pre-processing
        processed_inputs = self._preprocess_inputs(inputs)
        
        # Execute agent
        result = super()._call(processed_inputs, run_manager)
        
        # Post-processing
        final_result = self._postprocess_result(result)
        
        return final_result
    
    def _preprocess_inputs(self, inputs):
        # Add custom preprocessing
        return inputs
    
    def _postprocess_result(self, result):
        # Add custom postprocessing
        return result

custom_executor = CustomAgentExecutor.from_agent_and_tools(
    agent=agent,
    tools=tools,
    verbose=True
)
```

### Advanced Agent Patterns

#### Multi-Agent Systems

```python
from langchain.agents import initialize_agent
from langchain.tools import tool

# Specialized agents
@tool
def research_agent(query: str) -> str:
    """Research information."""
    research_llm = OpenAI(temperature=0.1)
    return research_llm(f"Research: {query}")

@tool
def analysis_agent(data: str) -> str:
    """Analyze data."""
    analysis_llm = OpenAI(temperature=0.5)
    return analysis_llm(f"Analyze: {data}")

# Coordinator agent
coordinator_tools = [research_agent, analysis_agent]
coordinator = initialize_agent(
    coordinator_tools,
    llm,
    agent="zero-shot-react-description"
)

# Usage
result = coordinator.run("Research AI trends and analyze their impact")
```

#### Agent with Learning

```python
from langchain.agents import Agent
from langchain.memory import ConversationBufferMemory

class LearningAgent(Agent):
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.memory = ConversationBufferMemory()
        self.learning_data = {}
    
    def learn_from_interaction(self, input_text, action, result):
        """Learn from successful interactions."""
        key = f"{input_text}_{action}"
        self.learning_data[key] = result
    
    def get_learned_response(self, input_text, action):
        """Retrieve learned response."""
        key = f"{input_text}_{action}"
        return self.learning_data.get(key)
```

---

## Database Integrations

Database integrations connect LangChain applications to structured data sources. These integrations let you query SQL databases, NoSQL stores, and custom data connectors directly from LLM-powered workflows. This is useful for analytics, reporting, searching, and updating persistent data.

### SQL Database Integration

```python
from langchain.utilities import SQLDatabase
from langchain.agents import create_sql_agent
from langchain.agents.agent_types import AgentType

# Connect to PostgreSQL database
db = SQLDatabase.from_uri("postgresql://user:password@localhost:5432/example_db")

# Create SQL agent
agent = create_sql_agent(
    llm=llm,
    db=db,
    agent_type=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)

# Query database
result = agent.run("How many users are there?")
```

### Vector Database Integration

```python
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings

# Connect to PostgreSQL with pgvector
connection_string = "postgresql://user:password@localhost:5432/dbname"

# Create vector store
embeddings = OpenAIEmbeddings()
vectorstore = PGVector(
    connection_string=connection_string,
    collection_name="Document",
    embedding_function=embeddings
)

# Add documents with metadata
vectorstore.add_texts(
    texts=["Document content"],
    metadatas=[{"source": "example"}]
)
```

### NoSQL Database Integration

```python
from langchain.document_loaders import MongoDBLoader

# Load from MongoDB
loader = MongoDBLoader(
    connection_string="mongodb://localhost:27017",
    db_name="mydatabase",
    collection_name="mycollection",
    field_name="text"
)

documents = loader.load()
```

### Custom Database Connectors

```python
from langchain.utilities import BaseDatabase
from typing import List, Dict, Any

class CustomDatabase(BaseDatabase):
    def __init__(self, connection_string: str):
        self.connection_string = connection_string
        # Initialize connection
    
    def run(self, query: str) -> str:
        # Execute query
        return f"Results for: {query}"
    
    def get_table_info(self) -> str:
        # Return schema information
        return "Table schema information"
    
    def run_query(self, query: str) -> List[Dict[str, Any]]:
        # Execute query and return results
        return [{"column": "value"}]
```

---

## API Integrations

API integrations enable LangChain agents and chains to interact with external services. You can call REST or GraphQL endpoints, process webhook events, and authorize requests using OAuth. This extends LLM applications to real-world data, SaaS platforms, and business workflows.

### REST API Integration

```python
import requests
from langchain.tools import tool

@tool
def api_call(endpoint: str, method: str = "GET", data: dict = None) -> str:
    """Make API calls."""
    try:
        if method == "GET":
            response = requests.get(endpoint)
        elif method == "POST":
            response = requests.post(endpoint, json=data)
        else:
            return f"Unsupported method: {method}"
        
        return response.json()
    except Exception as e:
        return f"API call failed: {str(e)}"

tools = [api_call]
agent = initialize_agent(tools, llm, agent="zero-shot-react-description")
```

### GraphQL API Integration

```python
from gql import gql, Client
from gql.transport.requests import RequestsHTTPTransport

@tool
def graphql_query(query: str, variables: dict = None) -> str:
    """Execute GraphQL queries."""
    transport = RequestsHTTPTransport(
        url="https://api.example.com/graphql",
        headers={"Authorization": "Bearer token"}
    )
    
    client = Client(transport=transport, fetch_schema_from_transport=True)
    
    try:
        result = client.execute(gql(query), variable_values=variables)
        return str(result)
    except Exception as e:
        return f"GraphQL query failed: {str(e)}"
```

### Webhook Integration

```python
from flask import Flask, request
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

app = Flask(__name__)

@app.route('/webhook', methods=['POST'])
def handle_webhook():
    data = request.json
    
    # Process webhook data with LangChain
    prompt = PromptTemplate(
        input_variables=["webhook_data"],
        template="Analyze this webhook data: {webhook_data}"
    )
    
    chain = LLMChain(llm=llm, prompt=prompt)
    analysis = chain.run(webhook_data=str(data))
    
    return {"analysis": analysis}

if __name__ == '__main__':
    app.run(debug=True)
```

### OAuth Integration

```python
from authlib.integrations.requests_client import OAuth2Session

class OAuthTool(BaseTool):
    name = "oauth_api"
    description = "Access OAuth-protected APIs"
    
    def __init__(self, client_id, client_secret, token_url):
        self.client_id = client_id
        self.client_secret = client_secret
        self.token_url = token_url
        self.session = None
    
    def authenticate(self):
        self.session = OAuth2Session(
            client_id=self.client_id,
            client_secret=self.client_secret
        )
        # Handle OAuth flow
    
    def _run(self, query: str) -> str:
        if not self.session:
            self.authenticate()
        
        # Make authenticated request
        response = self.session.get(f"https://api.example.com/{query}")
        return response.json()
```

---

## Memory Management

Memory management in LangChain defines how an application retains context across interactions. Different memory types control how much history is stored, whether it is summarized, and how it is exposed to chains and agents. Effective memory design helps produce coherent conversational AI and stateful workflows.

### Conversation Memory Types

#### ConversationBufferMemory

Stores entire conversation history.

```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain

memory = ConversationBufferMemory()
chain = ConversationChain(llm=llm, memory=memory)

chain.predict(input="Hi, I'm Alice.")
chain.predict(input="What's my name?")
```

#### ConversationBufferWindowMemory

Stores only recent messages.

```python
from langchain.memory import ConversationBufferWindowMemory

memory = ConversationBufferWindowMemory(k=2)  # Keep last 2 interactions
chain = ConversationChain(llm=llm, memory=memory)
```

#### ConversationSummaryMemory

Summarizes conversation history.

```python
from langchain.memory import ConversationSummaryMemory

memory = ConversationSummaryMemory(llm=llm)
chain = ConversationChain(llm=llm, memory=memory)
```

#### ConversationEntityMemory

Tracks entities mentioned in conversation.

```python
from langchain.memory import ConversationEntityMemory

memory = ConversationEntityMemory(llm=llm)
chain = ConversationChain(llm=llm, memory=memory)
```

### Custom Memory

Create custom memory classes.

```python
from langchain.memory import BaseMemory
from langchain.schema import BaseMemory
from typing import Dict, Any

class CustomMemory(BaseMemory):
    memory_key = "custom_memory"
    
    def __init__(self, **kwargs):
        super().__init__(**kwargs)
        self.custom_data = {}
    
    @property
    def memory_variables(self) -> List[str]:
        return [self.memory_key]
    
    def load_memory_variables(self, inputs: Dict[str, Any]) -> Dict[str, Any]:
        return {self.memory_key: self.custom_data}
    
    def save_context(self, inputs: Dict[str, Any], outputs: Dict[str, Any]) -> None:
        # Save context logic
        self.custom_data.update(inputs)
        self.custom_data.update(outputs)
    
    def clear(self) -> None:
        self.custom_data = {}
```

### Memory in Agents

```python
from langchain.agents import initialize_agent
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory(memory_key="chat_history", return_messages=True)

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.CHAT_CONVERSATIONAL_REACT_DESCRIPTION,
    memory=memory,
    verbose=True
)
```

---

## Document Loading and Processing

Document loading and processing are the first steps in building retrieval-based LangChain applications. Loaders ingest raw content from files, web pages, APIs, or databases; splitters and transformers clean and chunk that content for indexing and retrieval.

### Document Loaders

Load documents from various sources.

```python
from langchain.document_loaders import TextLoader, PyPDFLoader, WebBaseLoader

# Load text file
loader = TextLoader("document.txt")
documents = loader.load()

# Load PDF
loader = PyPDFLoader("document.pdf")
documents = loader.load()

# Load from web
loader = WebBaseLoader("https://example.com")
documents = loader.load()
```

### Text Splitters

Split documents into chunks.

```python
from langchain.text_splitter import CharacterTextSplitter, RecursiveCharacterTextSplitter

# Character-based splitting
text_splitter = CharacterTextSplitter(
    separator="\n\n",
    chunk_size=1000,
    chunk_overlap=200
)

# Recursive splitting
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200,
    separators=["\n\n", "\n", " ", ""]
)

chunks = text_splitter.split_documents(documents)
```

### Document Transformers

Transform documents.

```python
from langchain.document_transformers import EmbeddingsRedundantFilter
from langchain.embeddings import OpenAIEmbeddings

embeddings = OpenAIEmbeddings()
filter = EmbeddingsRedundantFilter(embeddings=embeddings)

filtered_docs = filter.transform_documents(documents)
```

---

## Vector Stores and Embeddings

Embeddings convert text into numerical vectors that capture semantic meaning. Vector stores index these embeddings and enable fast similarity search. This combination is the foundation of retrieval-augmented generation and intelligent document search.

### Embeddings

Convert text to vector representations.

```python
from langchain.embeddings import OpenAIEmbeddings, HuggingFaceEmbeddings

# OpenAI embeddings
embeddings = OpenAIEmbeddings()

# Hugging Face embeddings
embeddings = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)

# Generate embeddings
vectors = embeddings.embed_documents(["Hello world", "How are you?"])
query_vector = embeddings.embed_query("Greetings")
```

### Vector Stores

Store and search vectors.

#### PGVector

```python
from langchain.vectorstores import PGVector

# Connection string for PostgreSQL with pgvector extension
connection_string = "postgresql://user:password@localhost:5432/dbname"

# Create vector store
vectorstore = PGVector.from_documents(
    documents, 
    embeddings, 
    connection_string=connection_string,
    collection_name="my_collection"
)

# Search
results = vectorstore.similarity_search("query", k=5)
results_with_scores = vectorstore.similarity_search_with_score("query", k=5)
```

### Vector Store Operations

```python
# Add documents
vectorstore.add_documents(new_documents)

# Delete documents
vectorstore.delete(ids=["doc_id_1", "doc_id_2"])

# Update documents
vectorstore.update_document("doc_id", updated_document)

# Get by ID
doc = vectorstore.get(["doc_id"])

# Search with filter
results = vectorstore.similarity_search(
    "query", 
    k=5, 
    filter={"source": "web"}
)
```

---

## Retrieval-Augmented Generation (RAG)

RAG combines retrieval of relevant documents with generation from an LLM. This approach grounds responses in real data, reduces hallucinations, and enables applications like document Q&A, knowledge assistants, and fact-based summarization.

### Basic RAG Pipeline

```python
from langchain.chains import RetrievalQA
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings

# Load and process documents
loader = TextLoader("documents.txt")
documents = loader.load()
text_splitter = CharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
chunks = text_splitter.split_documents(documents)

# Create vector store
embeddings = OpenAIEmbeddings()
connection_string = "postgresql://user:password@localhost:5432/dbname"
vectorstore = PGVector.from_documents(chunks, embeddings, connection_string=connection_string, collection_name="rag_docs")

# Create retriever
retriever = vectorstore.as_retriever(search_kwargs={"k": 3})

# Create RAG chain
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True
)

# Query
result = qa_chain({"query": "What is the main topic?"})
print(result["result"])
print("Sources:", result["source_documents"])
```

### Advanced RAG Techniques

#### Multi-Query Retrieval

```python
from langchain.retrievers import MultiQueryRetriever

retriever = MultiQueryRetriever.from_llm(
    retriever=vectorstore.as_retriever(),
    llm=llm
)

docs = retriever.get_relevant_documents("What is machine learning?")
```

#### Contextual Compression

```python
from langchain.retrievers import ContextualCompressionRetriever
from langchain.retrievers.document_compressors import LLMChainExtractor

compressor = LLMChainExtractor.from_llm(llm)
compression_retriever = ContextualCompressionRetriever(
    base_compressor=compressor,
    base_retriever=retriever
)

compressed_docs = compression_retriever.get_relevant_documents("query")
```

#### Ensemble Retrieval

```python
from langchain.retrievers import EnsembleRetriever

retriever1 = vectorstore1.as_retriever()
retriever2 = vectorstore2.as_retriever()

ensemble_retriever = EnsembleRetriever(
    retrievers=[retriever1, retriever2],
    weights=[0.5, 0.5]
)
```

### RAG with Conversational Memory

```python
from langchain.chains import ConversationalRetrievalChain

qa_chain = ConversationalRetrievalChain.from_llm(
    llm=llm,
    retriever=retriever,
    memory=ConversationBufferMemory(
        memory_key="chat_history",
        return_messages=True
    )
)

result = qa_chain({"question": "What is the capital of France?"})
result = qa_chain({"question": "What about its population?"})
```

---

## Advanced Topics

This section covers advanced LangChain features for production-ready applications. It includes execution callbacks, streaming responses, asynchronous operation, custom component creation, and evaluation techniques for robust systems.

### Callbacks

Monitor and control chain execution.

```python
from langchain.callbacks import CallbackManager
from langchain.callbacks.base import BaseCallbackHandler

class CustomCallbackHandler(BaseCallbackHandler):
    def on_llm_start(self, serialized, prompts, **kwargs):
        print(f"LLM started with prompts: {prompts}")
    
    def on_llm_end(self, response, **kwargs):
        print(f"LLM finished with response: {response}")
    
    def on_chain_start(self, serialized, inputs, **kwargs):
        print(f"Chain started with inputs: {inputs}")
    
    def on_chain_end(self, outputs, **kwargs):
        print(f"Chain finished with outputs: {outputs}")

callback_manager = CallbackManager([CustomCallbackHandler()])
chain = LLMChain(llm=llm, prompt=prompt, callback_manager=callback_manager)
```

### Streaming

Stream responses in real-time.

```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

llm = OpenAI(
    streaming=True,
    callbacks=[StreamingStdOutCallbackHandler()]
)

chain = LLMChain(llm=llm, prompt=prompt)
chain.run(input="Tell me a story")
```

### Async Operations

Perform asynchronous operations.

```python
import asyncio
from langchain.chains import LLMChain

async def async_chain_run():
    result = await chain.arun(input="Hello world")
    return result

result = asyncio.run(async_chain_run())
```

### Custom Components

Create custom LangChain components.

#### Custom LLM

```python
from langchain.llms.base import LLM
from typing import Optional, List, Any

class CustomLLM(LLM):
    @property
    def _llm_type(self) -> str:
        return "custom"
    
    def _call(self, prompt: str, stop: Optional[List[str]] = None) -> str:
        # Custom LLM logic
        return f"Response to: {prompt}"
    
    async def _acall(self, prompt: str, stop: Optional[List[str]] = None) -> str:
        # Async version
        return f"Async response to: {prompt}"
```

#### Custom Prompt Template

```python
from langchain.prompts.base import BasePromptTemplate
from langchain.schema import PromptValue

class CustomPromptTemplate(BasePromptTemplate):
    template: str
    variables: List[str]
    
    def format(self, **kwargs) -> str:
        # Custom formatting logic
        return self.template.format(**kwargs)
    
    def format_prompt(self, **kwargs) -> PromptValue:
        return StringPromptValue(self.format(**kwargs))
```

### Evaluation and Metrics

```python
from langchain.evaluation import load_evaluator
from langchain.evaluation.criteria import Criteria

# Evaluate relevance
evaluator = load_evaluator("criteria", criteria=Criteria.RELEVANCE)
result = evaluator.evaluate_strings(
    prediction="Paris is the capital of France.",
    input="What is the capital of France?",
    reference="Paris"
)
print(result)

# Custom evaluation
def custom_evaluator(prediction, reference):
    # Custom evaluation logic
    return {
        "score": 0.85,
        "reasoning": "Good match but could be more detailed"
    }

# Evaluate chains
from langchain.evaluation import EvaluatorChain
eval_chain = EvaluatorChain.from_evaluator(custom_evaluator)
```

### Performance Benchmarking

```python
import time
from langchain.llms import OpenAI

def benchmark_llm(llm, prompts, iterations=10):
    """Benchmark LLM performance."""
    times = []
    
    for _ in range(iterations):
        start_time = time.time()
        responses = llm.generate(prompts)
        end_time = time.time()
        times.append(end_time - start_time)
    
    avg_time = sum(times) / len(times)
    tokens_per_second = sum(len(r.text.split()) for r in responses) / sum(times)
    
    return {
        "average_time": avg_time,
        "tokens_per_second": tokens_per_second,
        "total_tokens": sum(len(r.text.split()) for r in responses)
    }

prompts = ["Hello world"] * 5
results = benchmark_llm(llm, prompts)
print(f"Average time: {results['average_time']:.2f}s")
print(f"Tokens/second: {results['tokens_per_second']:.2f}")
```

---

## Business Use Cases and Applications

### Customer Support Automation

**Problem**: Companies receive thousands of customer inquiries daily, leading to long response times and high operational costs.

**LangChain Solution**:
```python
from langchain.agents import initialize_agent
from langchain.tools import tool
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings

@tool
def search_knowledge_base(query: str) -> str:
    """Search company knowledge base for relevant information."""
    # Implementation using vector store
    docs = vectorstore.similarity_search(query, k=3)
    return "\n".join([doc.page_content for doc in docs])

@tool
def escalate_to_human(ticket_id: str, reason: str) -> str:
    """Escalate complex issues to human agents."""
    # Implementation for ticket escalation
    return f"Ticket {ticket_id} escalated: {reason}"

@tool
def check_order_status(order_id: str) -> str:
    """Check order status in CRM system."""
    # Implementation for CRM integration
    return f"Order {order_id} status: Processing"

tools = [search_knowledge_base, escalate_to_human, check_order_status]
agent = initialize_agent(tools, llm, agent="zero-shot-react-description")

# Handle customer inquiry
response = agent.run("My order #12345 hasn't arrived yet. Can you help?")
```

**Benefits**:
- 24/7 availability
- Consistent responses
- Reduced operational costs
- Faster resolution times

### Content Generation for Marketing

**Problem**: Marketing teams struggle to create personalized content at scale for different customer segments.

**LangChain Solution**:
```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

# Multi-step content generation pipeline
research_prompt = PromptTemplate(
    input_variables=["topic", "audience"],
    template="""Research and analyze the topic: {topic} for {audience}.
    Provide key insights, trends, and talking points."""
)

content_prompt = PromptTemplate(
    input_variables=["research", "platform", "tone"],
    template="""Based on this research: {research}
    Create engaging content for {platform} with {tone} tone.
    Include compelling headline, body, and call-to-action."""
)

# Chain the prompts
research_chain = LLMChain(llm=llm, prompt=research_prompt)
content_chain = LLMChain(llm=llm, prompt=content_prompt)

# Generate content
research = research_chain.run(topic="AI in healthcare", audience="medical professionals")
content = content_chain.run(research=research, platform="LinkedIn", tone="professional")
```

**Benefits**:
- Personalized content at scale
- Consistent brand voice
- Faster content creation
- Data-driven insights

### Financial Analysis and Reporting

**Problem**: Financial analysts spend significant time gathering data and creating reports.

**LangChain Solution**:
```python
from langchain.agents import initialize_agent
from langchain.tools import tool
import yfinance as yf
import pandas as pd

@tool
def get_stock_data(symbol: str, period: str = "1y") -> str:
    """Fetch stock data from Yahoo Finance."""
    stock = yf.Ticker(symbol)
    data = stock.history(period=period)
    return data.to_string()

@tool
def calculate_financial_metrics(data: str) -> str:
    """Calculate key financial metrics."""
    df = pd.read_csv(pd.compat.StringIO(data), index_col=0)
    metrics = {
        "avg_price": df['Close'].mean(),
        "volatility": df['Close'].std(),
        "max_price": df['High'].max(),
        "min_price": df['Low'].min()
    }
    return str(metrics)

@tool
def generate_report(metrics: str, company: str) -> str:
    """Generate investment analysis report."""
    # Use LLM to create narrative report
    prompt = f"Based on these metrics for {company}: {metrics}, create an investment analysis report."
    return llm(prompt)

tools = [get_stock_data, calculate_financial_metrics, generate_report]
agent = initialize_agent(tools, llm, agent="zero-shot-react-description")

# Generate financial report
report = agent.run("Analyze Apple Inc. (AAPL) stock performance and create a report")
```

**Benefits**:
- Automated data analysis
- Consistent reporting format
- Reduced manual effort
- Real-time insights

### Legal Document Analysis

**Problem**: Lawyers and legal teams need to review extensive documents for relevant clauses and risks.

**LangChain Solution**:
```python
from langchain.document_loaders import PyPDFLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain.vectorstores import PGVector
from langchain.chains import RetrievalQA

# Load and process legal documents
loader = PyPDFLoader("contract.pdf")
documents = loader.load()

text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)
chunks = text_splitter.split_documents(documents)

# Create searchable vector store
embeddings = OpenAIEmbeddings()
connection_string = "postgresql://user:password@localhost:5432/dbname"
vectorstore = PGVector.from_documents(chunks, embeddings, connection_string=connection_string, collection_name="legal_docs")

# Create QA system for legal queries
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="map_reduce",
    retriever=vectorstore.as_retriever()
)

# Analyze contract
queries = [
    "What are the key termination clauses?",
    "Are there any indemnification provisions?",
    "What is the governing law?",
    "Identify potential risks in this contract"
]

for query in queries:
    answer = qa_chain.run(query)
    print(f"Query: {query}\nAnswer: {answer}\n")
```

**Benefits**:
- Faster document review
- Reduced human error
- Comprehensive analysis
- Risk identification

---

## Real-World Examples

### Chatbot with Memory

```python
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory
from langchain.prompts import PromptTemplate

template = """You are a helpful assistant. Use the following context to answer questions.

Current conversation:
{history}

Human: {input}
Assistant:"""

prompt = PromptTemplate(
    input_variables=["history", "input"],
    template=template
)

memory = ConversationBufferMemory()
chain = ConversationChain(
    llm=llm,
    prompt=prompt,
    memory=memory
)

while True:
    user_input = input("You: ")
    if user_input.lower() == "quit":
        break
    response = chain.predict(input=user_input)
    print(f"Bot: {response}")
```

### Document Q&A System

```python
from langchain.chains import RetrievalQA
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings
from langchain.text_splitter import RecursiveCharacterTextSplitter

# Load documents
from langchain.document_loaders import DirectoryLoader
loader = DirectoryLoader('./documents', glob="*.txt")
documents = loader.load()

# Split documents
text_splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,
    chunk_overlap=200
)
chunks = text_splitter.split_documents(documents)

# Create vector store
embeddings = OpenAIEmbeddings()
connection_string = "postgresql://user:password@localhost:5432/dbname"
vectorstore = PGVector.from_documents(chunks, embeddings, connection_string=connection_string, collection_name="qa_docs")

# Create QA chain
qa_chain = RetrievalQA.from_chain_type(
    llm=llm,
    chain_type="map_reduce",
    retriever=vectorstore.as_retriever()
)

# Interactive Q&A
while True:
    query = input("Ask a question: ")
    if query.lower() == "quit":
        break
    result = qa_chain.run(query)
    print(f"Answer: {result}")
```

### Code Generation Assistant

```python
from langchain.agents import initialize_agent, Tool
from langchain.tools import tool
from langchain.llms import OpenAI

@tool
def run_code(code: str) -> str:
    """Execute Python code and return the output."""
    try:
        exec_globals = {}
        exec(code, exec_globals)
        return "Code executed successfully"
    except Exception as e:
        return f"Error: {str(e)}"

@tool
def test_code(code: str) -> str:
    """Run tests on the provided code."""
    # Implementation for testing code
    return "Tests passed"

tools = [run_code, test_code]

llm = OpenAI(temperature=0.1)
agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent="zero-shot-react-description",
    verbose=True
)

agent.run("Write a Python function to calculate fibonacci numbers and test it")
```

### Research Assistant

```python
from langchain.tools import DuckDuckGoSearchRun
from langchain.agents import initialize_agent
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

# Research tools
search = DuckDuckGoSearchRun()
tools = [search]

# Research agent
agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent="zero-shot-react-description"
)

# Summarization chain
summary_prompt = PromptTemplate(
    input_variables=["research_data", "topic"],
    template="""Based on the following research data, provide a comprehensive summary of {topic}:

Research Data:
{research_data}

Summary:"""
)

summary_chain = LLMChain(llm=llm, prompt=summary_prompt)

# Research workflow
topic = "quantum computing applications"
research_data = agent.run(f"Research current applications of {topic}")
summary = summary_chain.run(research_data=research_data, topic=topic)

print(summary)
```

### Multi-Modal Assistant

```python
from langchain.tools import tool
from langchain.agents import initialize_agent
import base64

@tool
def analyze_image(image_path: str) -> str:
    """Analyze image content."""
    # Use vision model or image processing library
    return f"Image analysis of {image_path}"

@tool
def generate_image(prompt: str) -> str:
    """Generate image from text prompt."""
    # Use DALL-E or similar
    return f"Generated image for: {prompt}"

@tool
def text_to_speech(text: str) -> str:
    """Convert text to speech."""
    # Use TTS service
    return f"Audio generated for: {text}"

tools = [analyze_image, generate_image, text_to_speech]
agent = initialize_agent(tools, llm, agent="zero-shot-react-description")

agent.run("Create an image of a cat, analyze it, and generate speech describing it")
```

---

## Deployment and Production

Deployment and production guidance helps you run LangChain applications reliably and securely. This section covers containerization, API integration, scaling, monitoring, and caching strategies for real-world systems.

### Containerization with Docker

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "app.py"]
```

### FastAPI Integration

```python
from fastapi import FastAPI, HTTPException
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from pydantic import BaseModel

app = FastAPI()

class QueryRequest(BaseModel):
    query: str
    context: str = None

@app.post("/chat")
async def chat(request: QueryRequest):
    try:
        if request.context:
            prompt = PromptTemplate(
                input_variables=["query", "context"],
                template="Context: {context}\n\nQuestion: {query}\n\nAnswer:"
            )
            chain = LLMChain(llm=llm, prompt=prompt)
            result = chain.run(query=request.query, context=request.context)
        else:
            result = llm(request.query)
        
        return {"response": result}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))

@app.post("/agent")
async def run_agent(request: QueryRequest):
    try:
        result = agent.run(request.query)
        return {"response": result}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))
```

### Scaling with Load Balancing

```python
# Using Gunicorn for production
# gunicorn app:app -w 4 -k uvicorn.workers.UvicornWorker

# Kubernetes deployment
apiVersion: apps/v1
kind: Deployment
metadata:
  name: langchain-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: langchain-app
  template:
    metadata:
      labels:
        app: langchain-app
    spec:
      containers:
      - name: langchain-app
        image: your-registry/langchain-app:latest
        ports:
        - containerPort: 8000
        env:
        - name: OPENAI_API_KEY
          valueFrom:
            secretKeyRef:
              name: api-keys
              key: openai-api-key
```

### Monitoring and Observability

```python
from prometheus_client import Counter, Histogram, generate_latest
import time

REQUEST_COUNT = Counter('langchain_requests_total', 'Total requests', ['method', 'endpoint'])
REQUEST_LATENCY = Histogram('langchain_request_latency_seconds', 'Request latency', ['method', 'endpoint'])

def monitor_chain_execution(chain_func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        try:
            result = chain_func(*args, **kwargs)
            REQUEST_COUNT.labels(method='chain', endpoint='execute').inc()
            REQUEST_LATENCY.labels(method='chain', endpoint='execute').observe(time.time() - start_time)
            return result
        except Exception as e:
            REQUEST_COUNT.labels(method='chain', endpoint='error').inc()
            raise e
    return wrapper

@app.get("/metrics")
def metrics():
    return generate_latest()
```

### Caching Strategies

```python
from langchain.cache import RedisCache
from redis import Redis

# Redis caching
redis_client = Redis(host='localhost', port=6379, db=0)
set_llm_cache(RedisCache(redis_client))

# Custom cache with TTL
class TTLCache(BaseCache):
    def __init__(self, ttl_seconds=3600):
        self.cache = {}
        self.ttl = ttl_seconds
    
    def lookup(self, prompt, llm_string):
        key = self._key(prompt, llm_string)
        if key in self.cache:
            entry = self.cache[key]
            if time.time() - entry['timestamp'] < self.ttl:
                return entry['response']
            else:
                del self.cache[key]
        return None
    
    def update(self, prompt, llm_string, response):
        key = self._key(prompt, llm_string)
        self.cache[key] = {
            'response': response,
            'timestamp': time.time()
        }
```

---

## Security and Privacy

Security and privacy are critical for LLM applications. This section explains how to sanitize user input, manage API keys securely, apply rate limits, and protect private or sensitive data when using LangChain.

### Input Sanitization

```python
import re
from langchain.prompts import PromptTemplate

def sanitize_input(text: str) -> str:
    """Sanitize user input to prevent injection attacks."""
    # Remove potentially harmful patterns
    text = re.sub(r'<script[^>]*>.*?</script>', '', text, flags=re.IGNORECASE)
    text = re.sub(r'javascript:', '', text, flags=re.IGNORECASE)
    text = re.sub(r'on\w+\s*=', '', text, flags=re.IGNORECASE)
    
    # Limit length
    return text[:1000] if len(text) > 1000 else text

class SecurePromptTemplate(PromptTemplate):
    def format(self, **kwargs):
        # Sanitize all inputs
        sanitized_kwargs = {k: sanitize_input(str(v)) for k, v in kwargs.items()}
        return super().format(**sanitized_kwargs)
```

### API Key Management

```python
import os
from cryptography.fernet import Fernet

class SecureAPIKeyManager:
    def __init__(self, key_file='encryption.key'):
        self.key_file = key_file
        self.cipher = self._load_or_create_key()
    
    def _load_or_create_key(self):
        if os.path.exists(self.key_file):
            with open(self.key_file, 'rb') as f:
                key = f.read()
        else:
            key = Fernet.generate_key()
            with open(self.key_file, 'wb') as f:
                f.write(key)
        return Fernet(key)
    
    def encrypt_api_key(self, api_key: str) -> str:
        return self.cipher.encrypt(api_key.encode()).decode()
    
    def decrypt_api_key(self, encrypted_key: str) -> str:
        return self.cipher.decrypt(encrypted_key.encode()).decode()

# Usage
key_manager = SecureAPIKeyManager()
encrypted_key = key_manager.encrypt_api_key("sk-your-api-key")
# Store encrypted_key securely

# Later, decrypt when needed
api_key = key_manager.decrypt_api_key(encrypted_key)
os.environ["OPENAI_API_KEY"] = api_key
```

### Rate Limiting

```python
from functools import wraps
import time
from collections import defaultdict

class RateLimiter:
    def __init__(self, max_calls_per_minute=60):
        self.max_calls = max_calls_per_minute
        self.calls = defaultdict(list)
    
    def __call__(self, func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            now = time.time()
            user_id = kwargs.get('user_id', 'anonymous')
            
            # Clean old calls
            self.calls[user_id] = [call for call in self.calls[user_id] if now - call < 60]
            
            if len(self.calls[user_id]) >= self.max_calls:
                raise Exception("Rate limit exceeded")
            
            self.calls[user_id].append(now)
            return func(*args, **kwargs)
        return wrapper

rate_limiter = RateLimiter(max_calls_per_minute=10)

@rate_limiter
def process_user_query(query: str, user_id: str):
    return llm(query)
```

### Data Privacy

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

class PrivacyAwareChain(LLMChain):
    def __init__(self, *args, **kwargs):
        super().__init__(*args, **kwargs)
        self.privacy_filters = [
            self._filter_pii,
            self._filter_sensitive_topics
        ]
    
    def _filter_pii(self, text: str) -> str:
        """Remove or mask personally identifiable information."""
        import re
        # Simple PII patterns (in production, use more sophisticated NLP)
        patterns = [
            (r'\b\d{3}-\d{2}-\d{4}\b', '[SSN]'),  # SSN
            (r'\b\d{16}\b', '[CARD]'),  # Credit card
            (r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', '[EMAIL]')  # Email
        ]
        
        for pattern, replacement in patterns:
            text = re.sub(pattern, replacement, text)
        return text
    
    def _filter_sensitive_topics(self, text: str) -> str:
        """Filter sensitive topics."""
        sensitive_words = ['password', 'secret', 'confidential']
        for word in sensitive_words:
            text = text.replace(word, '[FILTERED]')
        return text
    
    def run(self, inputs, **kwargs):
        # Apply privacy filters to inputs
        filtered_inputs = {}
        for key, value in inputs.items():
            filtered_value = str(value)
            for filter_func in self.privacy_filters:
                filtered_value = filter_func(filtered_value)
            filtered_inputs[key] = filtered_value
        
        # Run chain with filtered inputs
        result = super().run(filtered_inputs, **kwargs)
        
        # Apply filters to output
        for filter_func in self.privacy_filters:
            result = filter_func(result)
        
        return result
```

### Secure Agent Design

```python
from langchain.agents import BaseSingleActionAgent
from langchain.schema import AgentAction, AgentFinish
from typing import List, Union, Any

class SecureAgent(BaseSingleActionAgent):
    def __init__(self, agent, security_policies):
        self.agent = agent
        self.security_policies = security_policies
    
    def plan(self, intermediate_steps, **kwargs):
        # Check security policies before planning
        input_text = kwargs.get('input', '')
        
        for policy in self.security_policies:
            if not policy.check(input_text):
                return AgentFinish(
                    return_values={"output": "Request blocked by security policy"},
                    log="Security policy violation"
                )
        
        # Proceed with normal planning
        return self.agent.plan(intermediate_steps, **kwargs)
    
    @property
    def input_keys(self):
        return self.agent.input_keys

class SecurityPolicy:
    def check(self, text: str) -> bool:
        """Return True if text passes security check."""
        # Implement security logic
        forbidden_words = ['hack', 'exploit', 'malware']
        return not any(word in text.lower() for word in forbidden_words)

# Usage
policies = [SecurityPolicy()]
secure_agent = SecureAgent(agent, policies)
```

---

## Best Practices and Optimization

Best practices in LangChain help you build maintainable, reliable, and efficient LLM applications. This section covers performance, caching, model selection, prompt hygiene, error handling, and deployment-ready design choices.

### Performance Optimization

#### Caching

```python
from langchain.cache import InMemoryCache
from langchain.globals import set_llm_cache

set_llm_cache(InMemoryCache())

# Now LLM responses will be cached
```

#### Batch Processing

```python
# Process multiple prompts at once
prompts = ["Prompt 1", "Prompt 2", "Prompt 3"]
responses = llm.generate(prompts)
```

#### Model Selection

```python
# Use smaller models for simple tasks
fast_llm = OpenAI(model_name="gpt-3.5-turbo", temperature=0.1)
complex_llm = OpenAI(model_name="gpt-4", temperature=0.7)
```

### Error Handling

```python
from langchain.llms import OpenAI
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(stop=stop_after_attempt(3), wait=wait_exponential(multiplier=1, min=4, max=10))
def call_llm_with_retry(prompt):
    try:
        return llm(prompt)
    except Exception as e:
        print(f"Error: {e}")
        raise

response = call_llm_with_retry("Hello world")
```

### Security Considerations

```python
# Sanitize inputs
def sanitize_input(user_input):
    # Remove potentially harmful content
    return user_input.replace("<script>", "").replace("</script>", "")

# Use environment variables for API keys
import os
api_key = os.getenv("OPENAI_API_KEY")
if not api_key:
    raise ValueError("API key not found")

# Limit token usage
llm = OpenAI(max_tokens=100, temperature=0.1)
```

### Testing

```python
import pytest
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate

def test_chain():
    prompt = PromptTemplate(input_variables=["input"], template="{input}")
    chain = LLMChain(llm=llm, prompt=prompt)
    
    # Mock the LLM for testing
    from unittest.mock import Mock
    chain.llm = Mock(return_value="Mock response")
    
    result = chain.run(input="test")
    assert result == "Mock response"
```

### Monitoring and Logging

```python
import logging
from langchain.callbacks import CallbackManager
from langchain.callbacks.base import BaseCallbackHandler

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class LoggingCallback(BaseCallbackHandler):
    def on_chain_end(self, outputs, **kwargs):
        logger.info(f"Chain completed with outputs: {outputs}")

callback_manager = CallbackManager([LoggingCallback()])
chain = LLMChain(llm=llm, prompt=prompt, callback_manager=callback_manager)
```

### Memory Optimization

```python
# Use efficient memory types
from langchain.memory import ConversationSummaryBufferMemory

memory = ConversationSummaryBufferMemory(
    llm=llm,
    max_token_limit=2000,
    return_messages=True
)

# Clear memory periodically
memory.clear()

# Optimize vector store memory usage
vectorstore = PGVector.from_documents(
    documents,
    embeddings,
    connection_string=connection_string,
    collection_name="optimized_docs"
)
```

### Cost Optimization

```python
# Track token usage
from langchain.callbacks import get_openai_callback

with get_openai_callback() as cb:
    result = chain.run(input="Expensive query")
    
print(f"Total tokens: {cb.total_tokens}")
print(f"Prompt tokens: {cb.prompt_tokens}")
print(f"Completion tokens: {cb.completion_tokens}")
print(f"Total cost: ${cb.total_cost}")

# Implement cost limits
class CostLimitedLLM:
    def __init__(self, llm, max_cost_per_day=10.0):
        self.llm = llm
        self.max_cost = max_cost_per_day
        self.daily_cost = 0.0
    
    def __call__(self, prompt):
        # Estimate cost (simplified)
        estimated_cost = len(prompt.split()) * 0.00002  # Rough estimate
        
        if self.daily_cost + estimated_cost > self.max_cost:
            raise Exception("Daily cost limit exceeded")
        
        result = self.llm(prompt)
        self.daily_cost += estimated_cost
        
        return result
```

---

## Troubleshooting

### Common Issues

#### API Key Errors

```python
# Check if API key is set
import os
if "OPENAI_API_KEY" not in os.environ:
    print("API key not found. Set OPENAI_API_KEY environment variable.")

# Verify API key format
api_key = os.environ.get("OPENAI_API_KEY", "")
if not api_key.startswith("sk-"):
    print("Invalid API key format")
```

#### Rate Limiting

```python
from tenacity import retry, stop_after_attempt, wait_exponential

@retry(stop=stop_after_attempt(5), wait=wait_exponential(multiplier=1, min=4, max=60))
def call_api():
    return llm("Hello")
```

#### Memory Issues

```python
# Clear memory periodically
memory.clear()

# Use windowed memory for long conversations
from langchain.memory import ConversationBufferWindowMemory
memory = ConversationBufferWindowMemory(k=10)
```

#### Import Errors

```python
# Check LangChain version
import langchain
print(f"LangChain version: {langchain.__version__}")

# Install missing dependencies
# pip install langchain[all]
```

### Debugging

```python
# Enable verbose mode
chain = LLMChain(llm=llm, prompt=prompt, verbose=True)

# Use debug mode
import langchain
langchain.debug = True

# Log all operations
import logging
logging.basicConfig(level=logging.DEBUG)
```

### Performance Issues

```python
# Profile chain execution
import cProfile
import pstats

def profile_chain():
    chain.run(input="Test input")

profiler = cProfile.Profile()
profiler.enable()
profile_chain()
profiler.disable()

stats = pstats.Stats(profiler)
stats.sort_stats('cumulative').print_stats(10)
```

### Integration Issues

```python
# Test integrations separately
try:
    # Test LLM
    response = llm("Hello")
    print("LLM working")
except Exception as e:
    print(f"LLM error: {e}")

try:
    # Test vector store
    vectorstore.similarity_search("test")
    print("Vector store working")
except Exception as e:
    print(f"Vector store error: {e}")

try:
    # Test agent
    agent.run("Test query")
    print("Agent working")
except Exception as e:
    print(f"Agent error: {e}")
```

---

## Resources and Further Reading

### Official Documentation

- [LangChain Documentation](https://python.langchain.com/)
- [LangChain GitHub](https://github.com/langchain-ai/langchain)
- [LangChain Hub](https://smith.langchain.com/hub)

### Tutorials and Guides

- [LangChain Tutorials](https://python.langchain.com/docs/get_started/introduction)
- [LangChain Cookbook](https://github.com/langchain-ai/langchain/tree/master/cookbook)
- [LangChain Examples](https://github.com/langchain-ai/langchain/tree/master/docs/docs/guides)

### Community Resources

- [LangChain Discord](https://discord.gg/langchain)
- [LangChain Twitter](https://twitter.com/LangChainAI)
- [LangChain Blog](https://blog.langchain.dev/)

### Related Libraries

- [LangChain Experimental](https://github.com/langchain-ai/langchain/tree/master/libs/experimental)
- [LangServe](https://github.com/langchain-ai/langserve)
- [LangSmith](https://smith.langchain.com/)

### Books and Courses

- "Building LLM Applications with LangChain" (upcoming)
- [DeepLearning.AI LangChain Course](https://www.deeplearning.ai/short-courses/langchain-for-llm-application-development/)

### Contributing

- [Contributing Guide](https://github.com/langchain-ai/langchain/blob/master/CONTRIBUTING.md)
- [Development Setup](https://github.com/langchain-ai/langchain/blob/master/README.md)

---

This ultra-comprehensive tutorial covers the fundamentals and advanced concepts of LangChain in Python. It includes detailed explanations, extensive code examples, best practices, security considerations, deployment strategies, and troubleshooting guides. Remember to experiment with the code examples and adapt them to your specific use cases. LangChain is a rapidly evolving framework, so stay updated with the latest documentation and releases.

### Built-in Agents

LangChain provides several pre-built agent types.

#### Zero-Shot ReAct Agent

```python
from langchain.agents import initialize_agent, AgentType
from langchain.tools import tool

@tool
def calculator(expression: str) -> str:
    """Evaluate a mathematical expression."""
    try:
        return str(eval(expression))
    except:
        return "Invalid expression"

tools = [calculator]

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,
    verbose=True
)

result = agent.run("What is 15 * 7 + 3?")
print(result)
```

#### Conversational Agent

```python
from langchain.agents import initialize_agent
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory(memory_key="chat_history")

agent = initialize_agent(
    tools=tools,
    llm=llm,
    agent=AgentType.CONVERSATIONAL_REACT_DESCRIPTION,
    memory=memory,
    verbose=True
)

agent.run("Hi, I'm Alice.")
agent.run("What's my name?")
```

### Custom Agents

Create agents with custom logic.

```python
from langchain.agents import Agent
from langchain.schema import AgentAction, AgentFinish
from typing import List, Tuple, Any, Union

class CustomAgent(Agent):
    @property
    def input_keys(self):
        return ["input"]
    
    def plan(self, intermediate_steps: List[Tuple[AgentAction, str]], **kwargs) -> Union[AgentAction, AgentFinish]:
        # Custom planning logic
        input_text = kwargs["input"]
        
        if "calculate" in input_text.lower():
            return AgentAction(tool="calculator", tool_input=input_text, log="Using calculator")
        else:
            return AgentFinish(
                return_values={"output": f"I don't know how to handle: {input_text}"},
                log="No appropriate tool found"
            )
```

### Tools

Tools are functions that agents can use.

#### Built-in Tools

```python
from langchain.tools import DuckDuckGoSearchRun, WikipediaQueryRun, WolframAlphaQueryRun

search = DuckDuckGoSearchRun()
wikipedia = WikipediaQueryRun()
wolfram = WolframAlphaQueryRun()

tools = [search, wikipedia, wolfram]
```

#### Custom Tools

```python
from langchain.tools import BaseTool
from typing import Optional

class CustomTool(BaseTool):
    name = "custom_tool"
    description = "A custom tool for demonstration"
    
    def _run(self, query: str) -> str:
        # Tool logic here
        return f"Processed: {query}"
    
    async def _arun(self, query: str) -> str:
        # Async version
        return f"Async processed: {query}"
```

#### Toolkits

Group related tools together.

```python
from langchain.agents import load_tools

# Load a toolkit
tools = load_tools(["serpapi", "llm-math"], llm=llm)

# Or create custom toolkit
from langchain.tools import Tool
from langchain.utilities import GoogleSearchAPIWrapper

search = GoogleSearchAPIWrapper()
tools = [
    Tool(
        name="Google Search",
        func=search.run,
        description="Search Google for information"
    )
]
```

---


### Callbacks

Monitor and control chain execution.

```python
from langchain.callbacks import CallbackManager
from langchain.callbacks.base import BaseCallbackHandler

class CustomCallbackHandler(BaseCallbackHandler):
    def on_llm_start(self, serialized, prompts, **kwargs):
        print(f"LLM started with prompts: {prompts}")
    
    def on_llm_end(self, response, **kwargs):
        print(f"LLM finished with response: {response}")
    
    def on_chain_start(self, serialized, inputs, **kwargs):
        print(f"Chain started with inputs: {inputs}")
    
    def on_chain_end(self, outputs, **kwargs):
        print(f"Chain finished with outputs: {outputs}")

callback_manager = CallbackManager([CustomCallbackHandler()])
chain = LLMChain(llm=llm, prompt=prompt, callback_manager=callback_manager)
```

### Streaming

Stream responses in real-time.

```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

llm = OpenAI(
    streaming=True,
    callbacks=[StreamingStdOutCallbackHandler()]
)

chain = LLMChain(llm=llm, prompt=prompt)
chain.run(input="Tell me a story")
```

### Async Operations

Perform asynchronous operations.

```python
import asyncio
from langchain.chains import LLMChain

async def async_chain_run():
    result = await chain.arun(input="Hello world")
    return result

result = asyncio.run(async_chain_run())
```

### Custom Components

Create custom LangChain components.

#### Custom LLM

```python
from langchain.llms.base import LLM
from typing import Optional, List, Any

class CustomLLM(LLM):
    @property
    def _llm_type(self) -> str:
        return "custom"
    
    def _call(self, prompt: str, stop: Optional[List[str]] = None) -> str:
        # Custom LLM logic
        return f"Response to: {prompt}"
    
    async def _acall(self, prompt: str, stop: Optional[List[str]] = None) -> str:
        # Async version
        return f"Async response to: {prompt}"
```

#### Custom Prompt Template

```python
from langchain.prompts.base import BasePromptTemplate
from langchain.schema import PromptValue

class CustomPromptTemplate(BasePromptTemplate):
    template: str
    variables: List[str]
    
    def format(self, **kwargs) -> str:
        # Custom formatting logic
        return self.template.format(**kwargs)
    
    def format_prompt(self, **kwargs) -> PromptValue:
        return StringPromptValue(self.format(**kwargs))
```

---

This comprehensive tutorial covers the fundamentals and advanced concepts of LangChain in Python. Remember to experiment with the code examples and adapt them to your specific use cases. LangChain is a rapidly evolving framework, so stay updated with the latest documentation and releases.