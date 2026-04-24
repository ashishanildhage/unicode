```python
import os
from langchain.llms import OpenAI

# Load your API key
os.environ["OPENAI_API_KEY"] = "your-key-here"
```

<a id="top"></a>
<style>
.back-to-top-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: #1f77b4;
  color: #ffffff;
  padding: 10px 14px;
  border-radius: 999px;
  text-decoration: none;
  font-weight: bold;
  box-shadow: 0 6px 18px rgba(0,0,0,0.18);
  z-index: 9999;
}
.back-to-top-button:hover {
  background: #155a8a;
}
</style>

<a href="#top" class="back-to-top-button">Back to Architecture</a>

## Learning Architecture

- [1. Core Building Blocks](#1-core-building-blocks)
  - [1.1 AI Models (LLMs and Chat)](#11-ai-models-llms-and-chat)
    - [1.1.a Text Completion Models (LLMs)](#111-text-completion-models-llms)
    - [1.1.b Chat Models](#112-chat-models)
    - [1.1.c Simple Prompts](#113-simple-prompts)
    - [1.1.d Chat Prompts](#114-chat-prompts)
  - [1.2 Chains: Linking Steps Together](#12-chains-linking-steps-together)
  - [1.3 Agents: Smart Decision Makers](#13-agents-smart-decision-makers)
  - [1.4 Memory: Remembering Conversations](#14-memory-remembering-conversations)
  - [1.5 Search and Retrieval: Finding Information](#15-search-and-retrieval-finding-information)
- [Working with Different AI Models](#working-with-different-ai-models)
  - [OpenAI](#openai)
  - [Anthropic (Claude)](#anthropic-claude)
  - [Hugging Face (free models)](#hugging-face-free-models)
- [Advanced Features](#advanced-features)
  - [Document Processing](#document-processing)
  - [Database Connections](#database-connections)
  - [Streaming and Async](#streaming-and-async)
- [Making Your App Production-Ready](#making-your-app-production-ready)
  - [Docker - Containerization](#docker---containerization)
  - [Error Handling](#error-handling)
  - [Monitoring](#monitoring)
- [Safety and Best Practices](#safety-and-best-practices)
  - [Input Sanitization](#input-sanitization)
  - [Rate Limiting](#rate-limiting)
  - [Secure API Keys](#secure-api-keys)
  - [Privacy Considerations](#privacy-considerations)
- [When Things Go Wrong](#when-things-go-wrong)
  - [Common Problems](#common-problems)
    - [API Key Issues](#api-key-issues)
    - [Rate Limits](#rate-limits)
    - [Memory Issues](#memory-issues)
    - [Import Errors](#import-errors)
  - [Debugging Tips](#debugging-tips)
- [Where to Learn More](#where-to-learn-more)
  - [Official Resources](#official-resources)
  - [Learning Paths](#learning-paths)
  - [Community](#community)
  - [Courses](#courses)
- [Prompt Engineering](#prompt-engineering)
  - [Basic Prompt Templates](#basic-prompt-templates)
  - [Few-Shot Prompting](#few-shot-prompting)
  - [Chat Prompt Templates](#chat-prompt-templates)
  - [Prompt Validation](#prompt-validation)
- [Chains in Depth](#chains-in-depth)
  - [LLMChain](#llmchain)
  - [Sequential Chains](#sequential-chains)
  - [Custom Chains](#custom-chains)
  - [Router Chains](#router-chains)
  - [Transformation Chains](#transformation-chains)
  - [Chain Composition Patterns](#chain-composition-patterns)
    - [Pipeline Pattern](#pipeline-pattern)
    - [Fan-out/Fan-in Pattern](#fan-outfan-in-pattern)
    - [Conditional Branching](#conditional-branching)
- [Agents and Tools](#agents-and-tools)
  - [Built-in Agents](#built-in-agents)
    - [Zero-Shot ReAct Agent](#zero-shot-react-agent)
    - [Conversational Agent](#conversational-agent)
    - [Structured Chat Agent](#structured-chat-agent)
  - [Custom Agents](#custom-agents)
  - [Tools](#tools)
    - [Built-in Tools](#built-in-tools)
    - [Custom Tools](#custom-tools)
    - [Toolkits](#toolkits)
  - [Agent Executors](#agent-executors)
  - [Advanced Agent Patterns](#advanced-agent-patterns)
    - [Multi-Agent Systems](#multi-agent-systems)
    - [Agent with Learning](#agent-with-learning)
- [Database Integrations](#database-integrations)
  - [SQL Database Integration](#sql-database-integration)
  - [Vector Database Integration](#vector-database-integration)
  - [NoSQL Database Integration](#nosql-database-integration)
  - [Custom Database Connectors](#custom-database-connectors)
- [API Integrations](#api-integrations)
  - [REST API Integration](#rest-api-integration)
  - [GraphQL API Integration](#graphql-api-integration)
  - [Webhook Integration](#webhook-integration)
  - [OAuth Integration](#oauth-integration)
- [Memory Management](#memory-management)
  - [Conversation Memory Types](#conversation-memory-types)
    - [ConversationBufferMemory](#conversationbuffermemory)
    - [ConversationBufferWindowMemory](#conversationbufferwindowmemory)
    - [ConversationSummaryMemory](#conversationsummarymemory)
    - [ConversationEntityMemory](#conversationentitymemory)
  - [Custom Memory](#custom-memory)
  - [Memory in Agents](#memory-in-agents)
- [Document Loading and Processing](#document-loading-and-processing)
  - [Document Loaders](#document-loaders)
  - [Text Splitters](#text-splitters)
  - [Document Transformers](#document-transformers)
- [Vector Stores and Embeddings](#vector-stores-and-embeddings)
  - [Embeddings](#embeddings)
  - [Vector Stores](#vector-stores)
    - [PGVector](#pgvector)
  - [Vector Store Operations](#vector-store-operations)
- [Retrieval-Augmented Generation (RAG)](#retrieval-augmented-generation-rag)
  - [Basic RAG Pipeline](#basic-rag-pipeline)
  - [Advanced RAG Techniques](#advanced-rag-techniques)
    - [Multi-Query Retrieval](#multi-query-retrieval)
    - [Contextual Compression](#contextual-compression)
    - [Ensemble Retrieval](#ensemble-retrieval)
  - [RAG with Conversational Memory](#rag-with-conversational-memory)
- [Advanced Topics](#advanced-topics)
  - [Callbacks](#callbacks)
  - [Streaming](#streaming)
  - [Async Operations](#async-operations)
  - [Custom Components](#custom-components)
    - [Custom LLM](#custom-llm)
    - [Custom Prompt Template](#custom-prompt-template)
  - [Evaluation and Metrics](#evaluation-and-metrics)
    - [Performance Benchmarking](#performance-benchmarking)
- [Business Use Cases and Applications](#business-use-cases-and-applications)
  - [Customer Support Automation](#customer-support-automation)
  - [Content Generation for Marketing](#content-generation-for-marketing)
  - [Financial Analysis and Reporting](#financial-analysis-and-reporting)
  - [Legal Document Analysis](#legal-document-analysis)
- [Real-World Examples](#real-world-examples)
  - [Chatbot with Memory](#chatbot-with-memory)
  - [Document Q&A System](#document-qa-system)
  - [Code Generation Assistant](#code-generation-assistant)
  - [Research Assistant](#research-assistant)
  - [Multi-Modal Assistant](#multi-modal-assistant)
- [Deployment and Production](#deployment-and-production)
  - [Containerization with Docker](#containerization-with-docker)
  - [FastAPI Integration](#fastapi-integration)
  - [Scaling with Load Balancing](#scaling-with-load-balancing)
  - [Monitoring and Observability](#monitoring-and-observability)
  - [Caching Strategies](#caching-strategies)
- [Security and Privacy](#security-and-privacy)
  - [Input Sanitization](#input-sanitization)
  - [API Key Management](#api-key-management)
  - [Rate Limiting](#rate-limiting)
  - [Data Privacy](#data-privacy)
  - [Secure Agent Design](#secure-agent-design)
- [Best Practices and Optimization](#best-practices-and-optimization)
  - [Performance Optimization](#performance-optimization)
    - [Caching](#caching)
    - [Batch Processing](#batch-processing)
    - [Model Selection](#model-selection)
  - [Error Handling](#error-handling)
  - [Security Considerations](#security-considerations)
  - [Testing](#testing)
  - [Monitoring and Logging](#monitoring-and-logging)
  - [Memory Optimization](#memory-optimization)
  - [Cost Optimization](#cost-optimization)
- [Troubleshooting](#troubleshooting)
  - [Common Issues](#common-issues)
    - [API Key Errors](#api-key-errors)
    - [Rate Limiting](#rate-limiting)
    - [Memory Issues](#memory-issues)
    - [Import Errors](#import-errors)
  - [Debugging](#debugging)
  - [Performance Issues](#performance-issues)
  - [Integration Issues](#integration-issues)
- [Resources and Further Reading](#resources-and-further-reading)
  - [Official Documentation](#official-documentation)
  - [Tutorials and Guides](#tutorials-and-guides)
  - [Community Resources](#community-resources)
  - [Related Libraries](#related-libraries)
  - [Books and Courses](#books-and-courses)
  - [Contributing](#contributing)

## Learning Architecture Diagram

### 📘 Learning Path Overview

1. **Core building blocks**
   - [AI Models](#11-ai-models-llms-and-chat): choose between text completion and chat.
   - [Prompts](#113-simple-prompts) and [Chat Prompts](#114-chat-prompts): teach the model what to do.
   - [Chains](#12-chains-linking-steps-together): connect steps into workflows.
   - [Agents](#13-agents-smart-decision-makers): add decision-making and tool use.
   - [Memory](#14-memory-remembering-conversations): retain context across turns.
   - [Search & Retrieval](#15-search-and-retrieval-finding-information): ground answers in your data.

2. **Expand with model options**
   - [OpenAI](#openai)
   - [Anthropic (Claude)](#anthropic-claude)
   - [Hugging Face](#hugging-face-free-models)

3. **Advanced features**
   - [Document processing](#document-processing)
   - [Database integration](#database-connections)
   - [Streaming & async](#streaming-and-async)

4. **Production architecture**
   - [Docker / Containerization](#docker---containerization)
   - [Error handling](#error-handling)
   - [Monitoring](#monitoring)
   - [Security](#safety-and-best-practices)
   - [Troubleshooting](#when-things-go-wrong)

### 🌲 Architecture Tree

- **[Core Building Blocks](#1-core-building-blocks)**
  - [AI Models](#11-ai-models-llms-and-chat)
    - Text Completion Models
    - Chat Models
  - [Prompts](#prompt-engineering)
    - [Simple Prompts](#113-simple-prompts)
    - [Chat Prompts](#114-chat-prompts)
  - [Chains](#12-chains-linking-steps-together)
    - [LLMChain](#llmchain)
    - [Sequential / Router / Custom Chains](#chains-in-depth)
  - [Agents](#13-agents-smart-decision-makers)
    - [Zero-Shot](#zero-shot-react-agent)
    - [Conversational](#conversational-agent)
    - [Structured Chat](#structured-chat-agent)
  - [Memory](#14-memory-remembering-conversations)
    - [Buffer](#conversationbuffermemory)
    - [Window](#conversationbufferwindowmemory)
    - [Summary](#conversationsummarymemory)
    - [Entity](#conversationentitymemory)
  - [Search & Retrieval](#15-search-and-retrieval-finding-information)
    - [Embeddings](#embeddings)
    - [Vector Store (PGVector)](#pgvector)
    - [Retriever](#15-search-and-retrieval-finding-information)
    - [RAG](#retrieval-augmented-generation-rag)

- **Core Extensions**
  - [Prompt Engineering](#prompt-engineering)
    - [Templates](#basic-prompt-templates)
    - [Few-shot](#few-shot-prompting)
    - [Validation](#prompt-validation)
  - [Chains in Depth](#chains-in-depth)
    - [Composition patterns](#chain-composition-patterns)
    - [Transformation chains](#transformation-chains)
  - [Agents and Tools](#agents-and-tools)
    - [Built-in Tools](#built-in-tools)
    - [Custom Tools](#custom-tools)
    - [Toolkits](#toolkits)
    - [Agent Executors](#agent-executors)

- **Data and Integration**
  - [Database Integrations](#database-integrations)
    - [SQL](#sql-database-integration)
    - [Vector DB](#vector-database-integration)
    - [NoSQL](#nosql-database-integration)
  - [API Integrations](#api-integrations)
    - [REST](#rest-api-integration)
    - [GraphQL](#graphql-api-integration)
    - [Webhooks](#webhook-integration)
    - [OAuth](#oauth-integration)
  - [Document Loading](#document-loading-and-processing)
    - [Loaders](#document-loaders)
    - [Splitters](#text-splitters)
    - [Transformers](#document-transformers)

- **Production & Optimization**
  - [Advanced Topics](#advanced-topics)
    - [Callbacks](#callbacks)
    - [Streaming](#streaming)
    - [Async Operations](#async-operations)
    - [Custom Components](#custom-components)
  - [Deployment](#deployment-and-production)
    - [Docker](#docker---containerization)
    - [FastAPI](#fastapi-integration)
    - [Scaling](#scaling-with-load-balancing)
    - [Observability](#monitoring-and-observability)
  - [Best Practices](#best-practices-and-optimization)
    - [Performance](#performance-optimization)
    - [Security](#security-and-privacy)
    - [Testing](#testing)
    - [Monitoring](#monitoring-and-logging)
    - [Cost](#cost-optimization)

- **Learning & Support**
  - [Business use cases](#business-use-cases-and-applications)
  - [Real-world examples](#real-world-examples)
  - [Security and privacy](#security-and-privacy)
  - [Troubleshooting](#troubleshooting)
  - [Resources and further reading](#resources-and-further-reading)

> **Top-level learning flow:**
> 1) Start with core concepts, 2) choose model + prompt style, 3) connect with chains and agents, 4) add memory + retrieval, 5) expand into integrations and production.

> **Tip:** Use the linked section names above to jump directly to each major topic and follow the tree branch that matches your project goals.

## 1. Core Building Blocks

  LangChain has 6 main concepts that you combine like building blocks. Think of them as ingredients in a recipe.

### 1.1 AI Models (LLMs and Chat)

These are the "brains" of your app. There are two main types:

<details>

<summary>1.1.a Text Completion Models (LLMs)</summary>

Good for single questions or generating text.

```python
from langchain.llms import OpenAI

llm = OpenAI()
story = llm("Write a short story about a robot")
print(story)
```

</details>

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

<details>

<summary>1.1.b Chat Models</summary>

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

</details>

<details>

<summary>1.1.c Simple Prompts</summary>

```python
from langchain.prompts import PromptTemplate

template = PromptTemplate(
    input_variables=["topic"],
    template="Explain {topic} like I'm 5 years old."
)

prompt = template.format(topic="artificial intelligence")
print(prompt)
```

</details>

<details>

<summary>1.1.d Chat Prompts</summary>

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

</details>


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

### Prompt Validation

**What is Prompt Validation?**
Prompt validation ensures that your templates are properly formatted and contain all required variables before they're used. This prevents runtime errors and ensures data quality.

**Why Validate Prompts?**
- **Catch errors early**: Identify issues before they reach the LLM
- **Type safety**: Ensure variables are the correct type
- **Consistency**: Enforce rules for all prompts in your application
- **User input protection**: Validate user inputs before inserting into templates

```python
from langchain.prompts import PromptTemplate
from pydantic import BaseModel, validator

# Create a custom prompt template with validation rules
class ValidatedPromptTemplate(PromptTemplate):
    """A prompt template that validates the template format."""
    
    @validator("template")  # This runs when the template is set
    def validate_template(cls, v):
        """Ensure template meets minimum requirements."""
        # Rule: Template must be at least 10 characters long
        if len(v) < 10:
            raise ValueError(
                "Template must be at least 10 characters long. "
                f"Your template is only {len(v)} characters."
            )
        return v

# Usage example:
try:
    # This will pass validation (> 10 characters)
    good_prompt = ValidatedPromptTemplate(
        input_variables=["topic"],
        template="Tell me about {topic} in detail."
    )
    print("✓ Prompt is valid!")
    
    # This will fail validation (< 10 characters)
    bad_prompt = ValidatedPromptTemplate(
        input_variables=["x"],
        template="About {x}"  # Only 8 characters
    )
except ValueError as e:
    print(f"✗ Validation error: {e}")
```

### 1.2 Chains: Linking Steps Together

**What are Chains?**
Chains connect multiple steps together in a workflow, similar to a recipe: mix ingredients → bake → cool. They allow you to:
- Combine multiple LangChain components into a reusable pipeline
- Pass outputs from one step as inputs to the next
- Maintain state and context across multiple processing steps
- Build complex workflows without writing complex boilerplate code

**Why Use Chains?**
- **Composability**: Easily combine prompts, LLMs, and tools
- **Reusability**: Define once, use many times
- **Maintainability**: Modify individual components without changing the overall workflow
- **Readability**: Clear, declarative syntax for multi-step processes

**Basic Chain Example:**
Here's a simple chain that takes a topic and generates a poem:

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI

# Step 1: Define the prompt template
# This template determines what question we ask the LLM
prompt = PromptTemplate(
    input_variables=["topic"],  # Variable to be filled in at runtime
    template="Write a poem about {topic}."  # Template with placeholder
)

# Step 2: Create the chain by linking the LLM and prompt
# The chain automatically handles passing outputs to inputs
chain = LLMChain(
    llm=OpenAI(),      # The AI model to use
    prompt=prompt      # The template to use
)

# Step 3: Execute the chain with a specific topic
# The input is automatically formatted into the template
poem = chain.run(topic="sunsets")
print(poem)  # Outputs a generated poem about sunsets
```

**How the chain works step-by-step:**
1. You provide `topic="sunsets"`
2. The prompt template formats this into: "Write a poem about sunsets."
3. This formatted text is sent to the LLM
4. The LLM generates a poem
5. The poem is returned to you

Chains abstract away this complexity so you can focus on the logic of your application.


LangChain provides several chain abstractions for sequential processing, branching, routing, and custom transformation logic.


### Sequential Chains

**What are Sequential Chains?**
Sequential chains run multiple chains one after another, where the output of one chain becomes the input to the next. This is useful for multi-step processes.

**Real-World Example:**
Imagine you want to:
1. Generate an interesting topic based on a subject
2. Write a full article about that generated topic

Instead of doing this manually, a sequential chain automates this workflow.

```python
from langchain.chains import SequentialChain, LLMChain
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI

# STEP 1: Create a chain to generate a topic
# ============================================
# This chain takes a subject and generates an interesting topic
topic_prompt = PromptTemplate(
    input_variables=["subject"],  # Input: subject (e.g., "machine learning")
    template="Generate an interesting topic related to {subject}."
)

topic_chain = LLMChain(
    llm=OpenAI(),
    prompt=topic_prompt,
    output_key="topic"  # IMPORTANT: Name the output so it can be referenced later
)

# STEP 2: Create a chain to write an article
# ==========================================
# This chain takes a topic and writes an article about it
article_prompt = PromptTemplate(
    input_variables=["topic"],  # Input: topic (will come from previous step)
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

**What are Transformation Chains?**
Transformation chains modify or clean input data before passing it to an LLM. They are useful for:
- Converting text to uppercase/lowercase
- Cleaning or formatting data
- Extracting information from raw input
- Preprocessing before sending to an LLM

**How They Work:**
1. Take raw input
2. Apply transformation function
3. Pass transformed output to next chain
4. Return final result

```python
from langchain.chains import TransformChain, LLMChain
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI

# Define a transformation function
# This function takes a dict and returns a dict
def transform_func(inputs: dict) -> dict:
    """
    Transform the input text by converting to uppercase.
    This is useful for standardizing data before LLM processing.
    
    Args:
        inputs: Dictionary with 'text' key containing raw text
        
    Returns:
        Dictionary with 'transformed_text' key containing uppercase text
    """
    text = inputs["text"]  # Get the raw text
    # Transformation logic: convert to uppercase
    transformed = text.upper()
    return {"transformed_text": transformed}  # Return as dict

# Create the transformation chain
transform_chain = TransformChain(
    input_variables=["text"],              # What input this chain expects
    output_variables=["transformed_text"], # What output it produces
    transform=transform_func               # The function to call
)

# Create an LLM chain that uses the transformed text
llm_prompt = PromptTemplate(
    input_variables=["transformed_text"],
    template="Summarize this text: {transformed_text}"
)

llm_chain = LLMChain(llm=OpenAI(), prompt=llm_prompt)

# Combine both chains
from langchain.chains import SimpleSequentialChain
overall_chain = SimpleSequentialChain(
    chains=[transform_chain, llm_chain],  # Run in order
    verbose=True                           # Show intermediate steps
)

# Usage: Raw text → Transformation → LLM → Summary
result = overall_chain.run("This is an important document we need to process")
print(result)  # Gets summary of uppercase version
```

**Execution Flow:**
```
Input: "This is an important document"
  → Transform: "THIS IS AN IMPORTANT DOCUMENT"
  → LLM Prompt: "Summarize this text: THIS IS AN IMPORTANT DOCUMENT"
  → Output: "[Summary from LLM]"
```


### 1.3 Agents: Smart Decision Makers

**What are Agents?**
Agents are AI systems that can:
- **Think and reason** about a problem
- **Choose which tools to use** (tools are functions they can call)
- **Decide when they have enough information** to answer
- **Try alternative approaches** if something fails

Unlike chains which follow a fixed path, agents dynamically decide what to do.

**Agent vs Chain:**
- **Chain**: Fixed sequence (Step 1 → Step 2 → Step 3)
- **Agent**: Dynamic thinking (Evaluate → Decide → Execute → Repeat as needed)

**How Agents Work (Step-by-Step):**
1. You ask a question
2. Agent thinks: "What tool would help answer this?"
3. Agent calls the appropriate tool
4. Agent receives tool output
5. Agent thinks: "Do I have the full answer now?"
6. If not, go back to step 2 with new information
7. If yes, provide final answer to user

**Simple Agent Example with Math:**
```python
from langchain.agents import initialize_agent, AgentType
from langchain.tools import tool
from langchain.llms import OpenAI

# Step 1: Define a tool - a function the agent can use
@tool
def multiply(a: int, b: int) -> int:
    \"""
    Multiply two numbers together.
    
    When: Use this when the user wants to multiply numbers
    Example: \"What is 15 times 7?\" → Use this tool
    \"""
    return a * b

# Step 2: Create the agent
agent = initialize_agent(
    tools=[multiply],                              # Toolbox: what agent can do
    llm=OpenAI(),                                  # Brain: how agent thinks
    agent=AgentType.ZERO_SHOT_REACT_DESCRIPTION,  # Strategy: how agent reasons
    verbose=True                                   # Show agent's thinking
)

# Step 3: Ask the agent a question
result = agent.run(\"What is 15 times 7?\")
\"\"\"\nAgent's Internal Process (shown with verbose=True):\n  Thought: \"I need to multiply 15 and 7\"\n  Action: multiply(a=15, b=7)\n  Observation: 105\n  Thought: \"I have the answer\"\n  Answer: \"15 times 7 equals 105\"\n\"\"\"\n```

**Real-World Agent Examples:**
OR
```python
@tool
def get_weather(city: str) -> str:
    """Get weather for a city."""
    response = requests.get(f"https://api.weather.com/{city}")
    return response.json()
# Now the Agent can get Weather live update.
```
OR 
```python
@tool
def check_order(order_id: str) -> str:
    """Check order status."""
    # Connect to your order database
    return f"Order {order_id} is shipped."

tools = [check_order]
agent = initialize_agent(tools, llm, agent="conversational-react-description")

response = agent.run("Where is my order #12345?")
```

**Tools agents can:** Search the web, Check databases, Send emails, Run code, Use APIs ...


### 1.4 Memory: Remembering Conversations

**Why Memory Matters:**
Without memory, AI treats each message as a fresh start:
- Turn 1: "Hi, I'm Alice" → AI processes
- Turn 2: "What's my name?" → AI has no idea (forgot Alice!)

With memory, AI maintains context:
- Turn 1: "Hi, I'm Alice" → AI stores: "user is Alice"
- Turn 2: "What's my name?" → AI retrieves: "You're Alice"

**How Memory Works:**
```
User: "Hi, I'm Alice"
  ↓ (stored in memory)
  [Memory Bank: {user_name: "Alice"}]
  
User: "What's my name?"
  ↓ (retrieved from memory)
  AI knows: "Alice" → Answers correctly
```

**Simple Memory Example:**
```python
from langchain.memory import ConversationBufferMemory
from langchain.chains import ConversationChain
from langchain.llms import OpenAI

# Create a memory store
# ConversationBufferMemory stores entire conversation history
memory = ConversationBufferMemory()

# Create a conversation chain with memory attached
conversation = ConversationChain(
    llm=OpenAI(),           # The AI model
    memory=memory,          # Attach memory for context
    verbose=True            # Show the full conversation
)

# Turn 1: Introduce yourself
response1 = conversation.predict(input="Hi, I'm Alice.")
# Memory stores: "User said: Hi, I'm Alice."
# AI responds: (acknowledges)

# Turn 2: AI uses memory
response2 = conversation.predict(input="What's my name?")
# Memory retrieves: "User said: Hi, I'm Alice."
# AI responds: "Your name is Alice."

# Turn 3: Can reference earlier context
response3 = conversation.predict(input="Can you help me with math?")
# AI remembers Alice and previous context
# AI responds with personalized help
```

**Memory Types Explained:**

1. **Buffer Memory** - Keeps everything
   - Use for: Short conversations, when you need full history
   - Pros: Complete context
   - Cons: Gets large with long conversations

2. **Window Memory** - Keeps only recent messages
   - Use for: Long conversations with space limitations
   - Example: Keep only last 5 messages
   - Pros: Limited memory usage
   - Cons: Loses old context

3. **Summary Memory** - Summarizes old messages
   - Use for: Very long conversations
   - Pros: Compact but keeps key info
   - Cons: Loses detail from older messages


### 1.5 Search and Retrieval: Finding Information

**The Problem Without Search:**
LLMs are trained on data from a certain time. They might give outdated or incorrect information:
- "What's the latest news?" → Can't answer (training data cutoff)
- "Tell me about Company X" → Might have wrong info
- "Summarize my documents" → No access to your files

**The Solution: Retrieval-Augmented Generation (RAG):**
```
User Question: "What is programming?"
  ↓
[1] SEARCH: Find relevant documents
  ↓
[2] COMBINE: Question + Found documents
  ↓
[3] ANSWER: AI generates answer based on facts
```

**How Vector Search Works:**
Instead of keyword matching, vector search finds meaning:
```
Question: "How to learn coding?"
  ↓ (convert to number pattern)
Vector: [0.2, -0.5, 0.8, 0.1, ...]

Document: "Python programming tutorial"
  ↓ (convert to number pattern)
Vector: [0.21, -0.48, 0.79, 0.09, ...]

Comparison: Vectors are very similar! → Match!
```

**Practical Implementation:**
```python
from langchain.vectorstores import PGVector
from langchain.embeddings import OpenAIEmbeddings
from langchain.document_loaders import TextLoader
from langchain.text_splitter import RecursiveCharacterTextSplitter

# STEP 1: Load and prepare documents
# =================================
loader = TextLoader("my_document.txt")
documents = loader.load()  # Load raw text

# Split large documents into chunks
# (LLMs handle small chunks better)
splitter = RecursiveCharacterTextSplitter(
    chunk_size=1000,      # Size of each chunk
    chunk_overlap=200     # Overlap to maintain context
)
chunks = splitter.split_documents(documents)

# STEP 2: Convert chunks to searchable vectors
# ===========================================
# Embeddings convert text to number patterns
embeddings = OpenAIEmbeddings()  # Use OpenAI's embedding model

# Create vector store (indexed and searchable)
connection_string = "postgresql://user:password@localhost:5432/dbname"
vectorstore = PGVector.from_documents(
    documents=chunks,                  # The chunks to index
    embedding=embeddings,              # Convert text to vectors
    connection_string=connection_string, # Where to store vectors
    collection_name="my_docs"          # Collection name
)

# STEP 3: Search documents
# ========================
query = "What is programming?"  # User's question
results = vectorstore.similarity_search(
    query,     # Search for this question
    k=3        # Return top 3 most similar documents
)

# Results are documents sorted by relevance
for doc in results:
    print(f"Found: {doc.page_content}")  # The relevant text
    print(f"Score: {doc.metadata.get('score', 'N/A')}")  # How relevant
```

**Complete RAG (Retrieval + Answering):**
```python
from langchain.chains import RetrievalQA

# Create a QA chain that uses retrieval
qa_chain = RetrievalQA.from_chain_type(
    llm=OpenAI(),                          # AI model for answering
    chain_type="stuff",                    # How to combine docs + question
    retriever=vectorstore.as_retriever()   # How to find relevant docs
)

# Ask questions - it automatically searches and answers
result = qa_chain({"query": "What is programming?"})
print(result["result"])  # AI-generated answer based on your documents
```

**RAG Workflow in Practice:**
```
User: "What is programming?"
  ↓
1. RETRIEVE: Find documents about programming
   Found: "Programming is writing instructions for computers"
         "Python is a programming language"
  ↓
2. COMBINE: Build prompt with docs + question
   Prompt: "Based on: [found documents]
             Answer this question: What is programming?"
  ↓
3. GENERATE: AI answers using the documents
   Answer: "Programming is the process of creating software...
             based on the provided documents, it includes..."
```

---

ADDINFO - RAG here 

---

## Working with Different AI Models

```python
# Anthropic (Claude)
from langchain.llms import Anthropic
llm = Anthropic()
# OR
llm = Anthropic(
    temperature=0.1,    # Low = consistent, High = creative
    max_tokens=100,     # Max response length
    model_name="gpt-4"  # Which model to use
)

# Hugging Face (free models)
from langchain.llms import HuggingFaceHub
llm = HuggingFaceHub(repo_id="google/flan-t5-base")
```

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

db = SQLDatabase.from_uri ("postgresql://user:password@localhost:5432/mydb")
# Now you can query your database with AI
```

### Streaming and Async

Get responses as they're generated (faster feel):

```python
from langchain.callbacks.streaming_stdout import StreamingStdOutCallbackHandler

llm = OpenAI (callbacks=[StreamingStdOutCallbackHandler()])
# Response appears character by character
```


---

## Making Your App Production-Ready

### Docker - Containerization 

Packaging app so it runs anywhere:

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

---

# Advanced detailed Tutorial




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

**What is Fan-out/Fan-in?**
Fan-out means splitting one input into multiple parallel operations. Fan-in means combining those results back together.

**Use Case:**
You want to analyze text in multiple ways and then combine all insights:
- **Fan-out**: One text → 3 different analyses
- **Fan-in**: 3 analysis results → Combined final assessment

```python
from langchain.chains import LLMChain
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI
import asyncio

# STEP 1: Define different analysis chains

# Analysis 1: Sentiment Analysis
sentiment_prompt = PromptTemplate(
    input_variables=["text"],
    template="Analyze the sentiment (positive/negative/neutral): {text}"
)
sentiment_chain = LLMChain(llm=OpenAI(), prompt=sentiment_prompt)

# Analysis 2: Entity Extraction  
entity_prompt = PromptTemplate(
    input_variables=["text"],
    template="Extract named entities (people, places, organizations): {text}"
)
entity_chain = LLMChain(llm=OpenAI(), prompt=entity_prompt)

# Analysis 3: Content Summarization
summary_prompt = PromptTemplate(
    input_variables=["text"],
    template="Provide a brief summary: {text}"
)
summary_chain = LLMChain(llm=OpenAI(), prompt=summary_prompt)

# STEP 2: Run all chains in parallel (fan-out)
async def run_parallel_analyses(text):
    # Run all analyses simultaneously
    sentiment_result = await sentiment_chain.arun(text=text)
    entity_result = await entity_chain.arun(text=text)
    summary_result = await summary_chain.arun(text=text)
    
    return sentiment_result, entity_result, summary_result

# STEP 3: Combine results (fan-in)
aggregate_prompt = PromptTemplate(
    input_variables=["sentiment", "entities", "summary"],
    template="""Combine these analyses into one assessment:
Sentiment: {sentiment}
Entities: {entities}
Summary: {summary}

Final assessment:"""
)

aggregate_chain = LLMChain(llm=OpenAI(), prompt=aggregate_prompt)

# Usage
async def complete_analysis(text):
    sentiment, entities, summary = await run_parallel_analyses(text)
    final = aggregate_chain.run(sentiment=sentiment, entities=entities, summary=summary)
    return final
```

**Benefits**: Parallel processing is faster, multiple perspectives give better insights

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



