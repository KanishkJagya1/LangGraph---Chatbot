# LangGraph AI Agent Examples

A comprehensive collection of LangGraph examples demonstrating how to build sophisticated AI agents with state management, tool integration, and human-in-the-loop capabilities.

## 🚀 Features

- **Basic Chatbot**: Simple conversational AI agent with LLM integration
- **Human-in-the-Loop**: AI agents that can request human assistance when needed
- **Tool Integration**: Web search and custom function capabilities
- **State Management**: Persistent conversation memory and context
- **Visual Graph Representation**: Mermaid diagrams for workflow visualization

## 📁 Project Structure

```
LangGraph/
├── basic Chatbot/
│   └── basicChatbot.ipynb          # Basic conversational agent
├── Human Assistance/
│   └── humanAssistance.ipynb       # Human-in-the-loop agent
├── main.py                         # Main entry point
├── pyproject.toml                  # Project configuration
├── requirements.txt                # Python dependencies
├── uv.lock                         # Dependency lock file
└── README.md                       # This file
```

## 🛠️ Installation

### Prerequisites

- Python 3.13 or higher
- [uv](https://docs.astral.sh/uv/) package manager (recommended)

### Setup

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd LangGraph
   ```

2. **Install dependencies**
   ```bash
   uv sync
   ```

3. **Set up environment variables**
   Create a `.env` file in the root directory:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   TAVILY_API_KEY=your_tavily_api_key_here
   ```

## 🎯 Examples

### 1. Basic Chatbot

The basic chatbot demonstrates a simple conversational agent using LangGraph:

- **Location**: `basic Chatbot/basicChatbot.ipynb`
- **Features**:
  - Direct LLM conversation
  - Tool integration (web search, custom functions)
  - Streaming responses
  - Graph visualization

**Key Components**:
```python
# State definition
class State(TypedDict):
    messages: Annotated[list, add_messages]

# Chatbot node
def chatbot(state: State):
    return {"messages": [llm.invoke(state["messages"])]}

# Graph construction
graph_builder = StateGraph(State)
graph_builder.add_node("llmchatbot", chatbot)
graph_builder.add_edge(START, "llmchatbot")
graph_builder.add_edge("llmchatbot", END)
```

### 2. Human-in-the-Loop Agent

Advanced agent that can request human assistance when needed:

- **Location**: `Human Assistance/humanAssistance.ipynb`
- **Features**:
  - Human assistance requests
  - Web search integration
  - Persistent memory with checkpoints
  - Conditional tool execution

**Key Components**:
```python
@tool
def human_assistance(query: str) -> str:
    """Request assistance from a human."""
    human_response = interrupt({"query": query})
    return human_response["data"]

# Memory and checkpointing
memory = MemorySaver()
graph = graph_builder.compile(checkpointer=memory)
```

## 🔧 Usage

### Running the Examples

1. **Basic Chatbot**:
   ```bash
   jupyter notebook "basic Chatbot/basicChatbot.ipynb"
   ```

2. **Human-in-the-Loop**:
   ```bash
   jupyter notebook "Human Assistance/humanAssistance.ipynb"
   ```

### Running the Main Application

```bash
python main.py
```

## 🛠️ Dependencies

### Core Dependencies
- `langgraph` - Stateful graph framework for AI agents
- `langchain` - Framework for developing applications with LLMs
- `langchain-groq` - Groq LLM integration
- `langchain-tavily` - Web search tool integration
- `langsmith` - LangChain observability and debugging
- `python-dotenv` - Environment variable management

### Development Dependencies
- `jupyter` - Interactive notebooks
- `ipython` - Enhanced Python shell

## 🔑 API Keys Required

To run the examples, you'll need:

1. **Groq API Key**: For LLM access (Llama 3.1 8B model)
   - Sign up at [Groq](https://console.groq.com/)
   - Add to `.env` as `GROQ_API_KEY`

2. **Tavily API Key**: For web search functionality
   - Sign up at [Tavily](https://tavily.com/)
   - Add to `.env` as `TAVILY_API_KEY`

## 🎨 Graph Visualization

Both examples include Mermaid diagram generation to visualize the agent workflows:

```python
from IPython.display import Image, display

try:
    display(Image(graph.get_graph().draw_mermaid_png()))
except Exception:
    pass
```

## 🔄 State Management

The agents use LangGraph's state management for:
- **Message History**: Persistent conversation context
- **Memory**: Long-term conversation storage
- **Checkpoints**: Resume conversations across sessions

## 🛡️ Error Handling

The examples include robust error handling for:
- API key validation
- Network connectivity issues
- Tool execution failures
- Human assistance timeouts

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

If you encounter any issues:

1. Check the [LangGraph documentation](https://langchain-ai.github.io/langgraph/)
2. Review the [LangChain documentation](https://python.langchain.com/)
3. Open an issue in this repository

## 🔮 Future Enhancements

- [ ] Multi-agent collaboration examples
- [ ] Database integration for persistent storage
- [ ] Web interface for human-in-the-loop interactions
- [ ] Advanced tool chaining examples
- [ ] Performance optimization guides

---

**Happy building with LangGraph! 🚀**
