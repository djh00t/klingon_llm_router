# Klingon LLM Router

Klingon LLM Router is a Python library designed to route Large Language Model (LLM) requests using semantic routing logic. It integrates with Semantic Router and provides a standardized API/backend interface for applications, allowing flexible routing based on configurable rulesets.

## Features

- **Semantic Routing**: Routes LLM requests based on YAML configuration using Semantic Router.
- **Flexible Routing Rules**: Supports routing based on costs, skills, skill levels, and fallback mechanisms.
- **Chromadb Integration**: Generates and stores chromadb embeddings of conversations for context-aware responses.
- **API Integration**: Provides access via public APIs (OpenAI, Google, Anthropic/Claude, Groq) and local models (llama, starcoder, mixtral) sourced from Hugging Face.
- **Environment Awareness**: Detects operating system and GPU resources to suggest appropriate models.

## Installation

Clone the repository and install dependencies:

```bash
git clone <repository-url>
cd klingon_llm_router
pip install -r requirements.txt
```

## Configuration

1. **config.yaml**: Configure routing rules and fallbacks.

    ```yaml
    # Example config.yaml
    routes:
      - name: least_cost_route
        condition: least_cost
        max_cost: 100
        destination: endpoint1

      - name: skilled_route
        condition: skill_level_at_least
        skill: language_understanding
        min_skill_level: 3
        destination: endpoint2

    fallback_llm: default_endpoint
    ```

2. **chromadb_config.yaml**: Configure chromadb location.

    ```yaml
    # Example chromadb_config.yaml
    chromadb_path: /path/to/chromadb
    ```

## Usage

### Initialize Router

```python
from klingon_llm_router import Router

# Initialize router with configuration files
router = Router(config_path='config/config.yaml', chromadb_config_path='config/chromadb_config.yaml')
```

### Route LLM Requests

```python
# Example LLM request
llm_request = {
    'type': 'query',
    'cost': 50,
    'skills': ['language_understanding', 'problem_solving'],
    'skill_levels': {'language_understanding': 4, 'problem_solving': 2}
}

# Route the request
response = router.route(llm_request)
print(response)
```

### Expected Outputs

- **Example Output for least_cost_route:**
  
  ```
  {'destination': 'endpoint1'}
  ```

- **Example Output for skilled_route:**
  
  ```
  {'destination': 'endpoint2'}
  ```

## Contributing

Contributions are welcome! For major changes, please open an issue first to discuss what you would like to change.

## License

[MIT License](LICENSE)
```

This template provides an overview of your `klingon_llm_router` project, including installation instructions, configuration details, usage examples, and expected outputs. Customize the placeholders (`<repository-url>`, paths, configurations) with your actual project details as you proceed with development. This README will help users understand how to use your library effectively.