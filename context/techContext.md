# AgentEvolve Technical Context

## Development Environment
- **Python**: 3.12
- **Environment**: `conda activate agent-evolve`
- **Base Framework**: OpenEvolve (forked, read-only)

## LLM Integration Matrix
| Phase | Primary Model | Secondary | Evaluator | API |
|-------|---------------|-----------|-----------|-----|
| PoT | Gemini 2.0 Flash | O1-mini-high | Gemini 2.5 | Google AI |
| PoC | Claude Sonnet 4 | Gemini 2.5 | O1-mini-high | AWS Bedrock |
| MVP | Multi-model Ensemble | Consensus | Specialized | Multiple |

## System Architecture

### Directory Structure
```bash
agent-evolve/
├── openevolve/                    # Forked OpenEvolve (DO NOT MODIFY)
├── pilot/                         # Phase 1: Basic functional evaluation
│   ├── config/base.yaml          # Gemini 2.0 configuration
│   ├── evaluators/correctness.py # Functional correctness checker
│   ├── tasks/fizzbuzz.py         # Initial coding task
│   └── run_pilot.py              # Entry point
├── claude/                        # Phase 2: Task completeness evaluation
│   ├── config/bedrock.yaml       # Claude Bedrock configuration
│   ├── agents/claude_bedrock.py  # Bedrock integration
│   ├── evaluators/deepeval.py    # Task completeness metrics
│   └── run_claude.py             # Entry point
└── agent/                         # Phase 3: Production pipeline
    ├── config/production.yaml    # Multi-model configuration
    ├── evaluation/cascade.py     # Multi-stage evaluator
    ├── evolution/map_elites.py   # Advanced algorithms
    └── run_agent.py              # Entry point
```

### API Integration Specifications

#### Phase 1: Google AI (Gemini)
```python
# pilot/llm/gemini_provider.py
import google.generativeai as genai

class GeminiProvider:
    def __init__(self):
        genai.configure(api_key=os.getenv('GOOGLE_API_KEY'))
        self.model = genai.GenerativeModel('gemini-2.0-flash-exp')
```

#### Phase 2: Claude via AWS Bedrock
```python
# claude/llm/bedrock_provider.py
import boto3

class ClaudeBedrockProvider:
    def __init__(self):
        self.bedrock = boto3.client(
            service_name='bedrock-runtime',
            region_name='us-east-1'
        )
        self.model_id = 'anthropic.claude-3-5-sonnet-20241022-v2:0'

    def generate(self, prompt: str) -> str:
        response = self.bedrock.invoke_model(
            modelId=self.model_id,
            body=json.dumps({
                'messages': [{'role': 'user', 'content': prompt}],
                'max_tokens': 4000,
                'temperature': 0.7
            })
        )
```

#### Phase 3: Multi-Model Ensemble
```python
# agent/llm/ensemble.py
class ModelEnsemble:
    def __init__(self):
        self.providers = {
            'gemini-2.5': GeminiProvider('gemini-2.5-flash-exp'),
            'claude-bedrock': ClaudeBedrockProvider(),
            'o1-mini': OpenAIProvider('o1-mini-2024-09-12')
        }
```

### Configuration Management

#### Environment Setup
```bash
# Python 3.12 environment
conda create -n agent-evolve python=3.12
conda activate agent-evolve

# Install dependencies
pip install -e ./openevolve
pip install google-generativeai boto3 deepeval openai
pip install docker pytest mypy black pylint
```

#### AWS Bedrock Configuration
```bash
# AWS credentials for Bedrock
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="us-east-1"

# Alternative: AWS CLI configuration
aws configure set region us-east-1
aws configure set aws_access_key_id your-access-key
aws configure set aws_secret_access_key your-secret-key
```

#### API Keys Configuration
```bash
export GOOGLE_API_KEY="your-gemini-key"
export OPENAI_API_KEY="your-openai-key"
# AWS credentials handled via AWS CLI or environment variables
```

### Performance Specifications
- **Memory**: 8GB minimum for multi-model inference
- **CPU**: 8+ cores for parallel evaluation
- **Python**: 3.12 with type hints and modern features
- **Concurrency**: asyncio for API calls, multiprocessing for evaluation

### Security Configuration
```python
# Bedrock IAM policy requirements
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "bedrock:InvokeModel"
            ],
            "Resource": [
                "arn:aws:bedrock:us-east-1::foundation-model/anthropic.claude-3-5-sonnet-20241022-v2:0"
            ]
        }
    ]
}
```

### Docker Integration (Phase 2+)
```dockerfile
FROM python:3.12-slim
RUN pip install boto3 google-generativeai
# Execution isolation for code evaluation
```

This technical context provides concrete implementation details for each phase while maintaining the high-level roadmap structure.
