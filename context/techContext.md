# AgentEvolve Technical Context

## Development Environment
- **Python**: 3.12
- **Environment**: `conda activate agent-evolve`
- **Base Framework**: OpenEvolve (direct pattern replication, no modifications)
- **Implementation Strategy**: Exact reuse of `openevolve/examples/function_minimization` patterns

## LLM Integration Matrix
| Phase | Primary Model | Secondary | Evolution Target | API |
|-------|---------------|-----------|------------------|-----|
| PoT ✅ | gemini-2.0-flash-lite | gemini-2.0-flash | FastAPI Backend | Google AI |
| PoC | Claude Sonnet 3.5 | Gemini 2.5 | Enhanced FastAPI | AWS Bedrock |
| MVP | Multi-model Ensemble | Consensus | Production API | Multiple |

## System Architecture

### Directory Structure
```bash
agent-evolve/
├── openevolve/                    # Forked OpenEvolve (DO NOT MODIFY)
├── pilot/                         # Phase 1: FastAPI backend evolution
│   ├── config.yaml               # OpenEvolve configuration (Gemini)
│   ├── initial_program.py         # FastAPI backend with EVOLVE-BLOCK
│   ├── evaluator.py              # HTTP endpoint testing system
│   ├── requirements.txt          # FastAPI dependencies
│   └── README.md                 # Complete documentation
├── claude/                        # Phase 2: Enhanced evaluation (planned)
└── agent/                         # Phase 3: Production pipeline (planned)
```

### API Integration Specifications

#### Phase 1: Google AI (OpenAI-Compatible)
```yaml
# pilot/config.yaml - OpenEvolve configuration format
llm:
  primary_model: "gemini-2.0-flash-lite"
  secondary_model: "gemini-2.0-flash"
  api_base: "https://generativelanguage.googleapis.com/v1beta/openai/"
  temperature: 0.7
  max_tokens: 4096
```

#### Phase 2: Claude via AWS Bedrock
```yaml
# claude/config.yaml - Same OpenEvolve pattern
llm:
  primary_model: "anthropic.claude-3-5-sonnet-20241022-v2:0"
  api_base: "bedrock"
  region: "us-east-1"
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

# Install OpenEvolve and FastAPI dependencies
cd agent-evolve
pip install -e ./openevolve
pip install -r pilot/requirements.txt
```

#### API Keys Configuration
```bash
export GOOGLE_API_KEY="your-gemini-key"
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
