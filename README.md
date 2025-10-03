# LangGraph Subgraphs Tutorial

A comprehensive guide demonstrating how to compose and integrate subgraphs in LangGraph applications, featuring a weather search agent with tool-calling capabilities.

## Overview

This project explores two different approaches to embedding subgraphs within parent graphs using LangGraph. It implements a practical weather search agent that uses the Tavily search tool to fetch real-time weather information.

## Features

- **Modular Subgraph Design**: Reusable search agent component with tool-calling capabilities
- **Multiple Integration Patterns**: Demonstrates both shared schema and schema transformation approaches
- **Tool Integration**: Built-in Tavily search tool for web queries
- **Memory Management**: Integrated checkpoint memory system
- **Agent-Tool Loop**: Automatic routing between agent reasoning and tool execution

## Architecture

### Subgraph Component
The search agent subgraph includes:
- Agent node with GPT-4 mini LLM
- Tool node for executing Tavily searches
- Conditional routing based on tool call requirements
- Automatic loop between agent and tools until task completion

### Integration Patterns

#### Pattern 1: Shared Schema (Direct Embedding)
When parent and child graphs share the same state schema, the subgraph can be directly embedded as a node.

#### Pattern 2: Different Schema (Transform & Invoke)
When schemas differ, transformation functions handle state conversion between parent and subgraph contexts.

## Prerequisites

- Python 3.8+
- OpenAI API key
- Tavily API key
- Jupyter Notebook environment

## Installation

```bash
pip install langgraph langchain langchain-openai langchain-community
pip install youtube-transcript-api pydantic python-dotenv
pip install faiss-cpu pymupdf arxiv
```

## Environment Setup

Create a `.env` file with your API keys:

```env
OPENAI_API_KEY=your_openai_key_here
TAVILY_API_KEY=your_tavily_key_here
```

## Usage

### Running the Notebook

Open `Subgraphs_LG.ipynb` in Jupyter and execute the cells sequentially to:

1. Initialize the search agent subgraph
2. Test the standalone subgraph functionality
3. Embed the subgraph using shared schema pattern
4. Integrate using schema transformation pattern

### Example Queries

```python
# Direct subgraph invocation
result = search_app.invoke({
    "messages": [HumanMessage(content="How is the weather in Lahore?")]
})

# Parent graph with shared schema
result = parent_app.invoke({
    "messages": [HumanMessage(content="How is the weather in Lahore?")]
})

# Parent graph with different schema
result = parent_app.invoke({
    "query": "How is the weather in Chennai?",
    "response": ""
})
```

## Technical Stack

- **LangGraph**: State machine and workflow orchestration
- **LangChain**: LLM framework and tool integration
- **OpenAI GPT-4 Mini**: Language model for agent reasoning
- **Tavily Search**: Real-time web search tool
- **FAISS**: Vector store for document retrieval
- **Pydantic**: Data validation and type checking

## Key Concepts

### State Management
- `ChildState`: Subgraph state with message history
- `ParentState`: Parent graph state (same as child in Pattern 1)
- `QueryState`: Parent graph state with custom schema (Pattern 2)

### Routing Logic
Conditional edges determine whether to:
- Continue to tool execution (when tool calls are present)
- End the conversation (when agent provides final answer)

### Tool Integration
The Tavily search tool provides:
- Real-time web search results
- Structured JSON responses
- URL references and content snippets

## Graph Visualization

The project includes visual representations of:
- Subgraph flow (agent → tool_node → agent → end)
- Integration patterns with parent graphs
- Message flow and state transformations

## Use Cases

- Weather information retrieval
- General web search queries
- Multi-step reasoning with tool use
- Composable agent architectures
- Reusable component design patterns

## Contributing

Feel free to explore different integration patterns, add new tools, or experiment with alternative state schemas.

## License

This project is provided as an educational resource for learning LangGraph subgraph composition patterns.

---

Built with LangGraph, LangChain, and OpenAI
