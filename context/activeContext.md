# AgentEvolve Active Development Context

## Current Implementation: Phase 1 PoT (`pilot/`)

### Technical Environment
- **Python**: 3.12
- **Conda Environment**: `agent-evolve`
- **Primary Model**: Gemini 2.0 Flash (`gemini-2.0-flash-exp`)
- **Evaluation Model**: Gemini 2.5 Flash (`gemini-2.5-flash-exp`)

### Active Directory Structure
```bash
pilot/
├── config/base.yaml              # Gemini configuration
├── evaluators/correctness.py     # Functional evaluation
├── tasks/fizzbuzz.py            # Initial coding task
├── llm/gemini_provider.py       # Google AI integration
└── run_pilot.py                 # Main execution
```

### Current Focus: OpenEvolve Extension Pattern

#### Configuration Extension
```yaml
# pilot/config/base.yaml
extends: "../../openevolve/config/default.yaml"
llm:
  provider: "gemini"
  model: "gemini-2.0-flash-exp"
  api_key_env: "GOOGLE_API_KEY"
  temperature: 0.7
population:
  size: 15
  max_iterations: 50
task:
  name: "fizzbuzz"
  type: "algorithmic"
```

#### API Integration Approach
```python
# pilot/llm/gemini_provider.py
import google.generativeai as genai
from openevolve.llm_interface import LLMProvider

class GeminiProvider(LLMProvider):
    def __init__(self, model_name: str):
        genai.configure(api_key=os.getenv('GOOGLE_API_KEY'))
        self.model = genai.GenerativeModel(model_name)

    def generate(self, prompt: str, **kwargs) -> str:
        response = self.model.generate_content(prompt)
        return response.text
```

### Phase Transition Planning

#### Phase 2 Preparation (`claude/`)
- **Claude Integration**: AWS Bedrock setup required
- **DeepEval Framework**: Task completeness evaluation
- **Docker Setup**: Execution isolation implementation

#### AWS Bedrock Requirements
```python
# claude/llm/bedrock_provider.py
import boto3
import json

class ClaudeBedrockProvider:
    def __init__(self):
        self.bedrock = boto3.client('bedrock-runtime', region_name='us-east-1')
        self.model_id = 'anthropic.claude-3-5-sonnet-20241022-v2:0'
```

### Development Commands

#### Environment Setup
```bash
conda create -n agent-evolve python=3.12
conda activate agent-evolve
pip install -e ./openevolve
pip install google-generativeai==0.8.0
```

#### Phase 1 Execution
```bash
cd agent-evolve/pilot
export GOOGLE_API_KEY="your-key"
python run_pilot.py --config config/base.yaml
```

#### Phase 2 Preparation
```bash
# AWS Bedrock setup
aws configure set region us-east-1
pip install boto3
# Test Bedrock connectivity
python -c "import boto3; print(boto3.client('bedrock-runtime').list_foundation_models())"
```

### Current Technical Priorities
1. **Gemini Integration**: Complete Google AI API setup
2. **FizzBuzz Implementation**: Define comprehensive test cases
3. **Evaluation Pipeline**: Functional correctness checker
4. **Evolution Loop**: Integration with OpenEvolve controller

### Success Metrics
- Gemini 2.0 Flash generates valid Python code
- FizzBuzz correctness improves over 20+ iterations
- Clean extension pattern without OpenEvolve modifications
- Ready for Phase 2 Bedrock integration

Focus: Prove evolutionary code improvement using Gemini models with clean architecture.
