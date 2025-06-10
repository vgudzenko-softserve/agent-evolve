# AgentEvolve Task Queue

## ACTIVE: Phase 1 PoT (`pilot/`) - Python 3.12

### 🔴 IMMEDIATE - Current Sprint

#### **AE-001**: Gemini 2.0 Integration
**Status**: IN PROGRESS
**Environment**: Python 3.12, `conda agent-evolve`

```python
# pilot/llm/gemini_provider.py
import google.generativeai as genai
import os

class GeminiProvider:
    def __init__(self, model_name="gemini-2.0-flash-exp"):
        genai.configure(api_key=os.getenv('GOOGLE_API_KEY'))
        self.model = genai.GenerativeModel(model_name)
```

**Subtasks**:
- [ ] Python 3.12 conda environment setup
- [ ] Google AI Python SDK installation
- [ ] Gemini API key configuration
- [ ] Basic generation test

---

#### **AE-002**: FizzBuzz Task Implementation
**Status**: READY TO START

```python
# pilot/tasks/fizzbuzz.py
TASK_SPEC = {
    "name": "fizzbuzz",
    "prompt": "Write a Python function that prints numbers 1-100...",
    "test_cases": [
        {"range": (1, 16), "expected": ["1", "2", "Fizz", "4", "Buzz", "Fizz", "7", "8", "Fizz", "Buzz", "11", "Fizz", "13", "14", "FizzBuzz"]},
        # Edge cases, boundary conditions
    ]
}
```

**Subtasks**:
- [ ] Comprehensive test case definition
- [ ] Initial program template
- [ ] Test runner implementation

---

#### **AE-003**: Functional Correctness Evaluator
**Status**: BLOCKED (waiting for AE-002)

```python
# pilot/evaluators/correctness.py
from openevolve.evaluation_result import EvaluationResult
import subprocess
import tempfile

class FunctionalCorrectnessEvaluator:
    def evaluate(self, program: str, task_spec: dict) -> EvaluationResult:
        # Execute program, check outputs against test cases
        pass
```

---

### 🟡 NEXT SPRINT - Phase 2 Prep (`claude/`)

#### **AE-004**: AWS Bedrock Setup
**Status**: PLANNED
**Dependency**: Phase 1 completion

```bash
# Environment preparation
pip install boto3==1.34.0
aws configure set region us-east-1
export AWS_ACCESS_KEY_ID="your-key"
export AWS_SECRET_ACCESS_KEY="your-secret"
```

**Implementation**:
```python
# claude/llm/bedrock_provider.py
import boto3
import json

class ClaudeBedrockProvider:
    def __init__(self):
        self.bedrock = boto3.client('bedrock-runtime', region_name='us-east-1')
        self.model_id = 'anthropic.claude-3-5-sonnet-20241022-v2:0'

    def generate(self, prompt: str) -> str:
        body = json.dumps({
            'messages': [{'role': 'user', 'content': prompt}],
            'max_tokens': 4000,
            'temperature': 0.7
        })
        response = self.bedrock.invoke_model(modelId=self.model_id, body=body)
        return json.loads(response['body'].read())['content'][0]['text']
```

---

#### **AE-005**: DeepEval Integration
**Status**: PLANNED

```python
# claude/evaluators/task_completeness.py
from deepeval import evaluate
from deepeval.metrics import TaskCompleteness

class TaskCompletenessEvaluator:
    def __init__(self):
        self.metric = TaskCompleteness(threshold=0.8)
```

---

## DEVELOPMENT ENVIRONMENT

### Python 3.12 Setup
```bash
conda create -n agent-evolve python=3.12
conda activate agent-evolve

# Core dependencies
pip install -e ./openevolve
pip install google-generativeai==0.8.0
pip install boto3==1.34.0
pip install deepeval==1.0.0
pip install pytest mypy black pylint
```

### API Configuration
```bash
# Phase 1: Google AI
export GOOGLE_API_KEY="your-gemini-key"

# Phase 2: AWS Bedrock
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="us-east-1"

# Phase 3: OpenAI (for O1-mini)
export OPENAI_API_KEY="your-openai-key"
```

### Execution Commands
```bash
# Phase 1
cd agent-evolve/pilot
python run_pilot.py --config config/base.yaml

# Phase 2 (future)
cd agent-evolve/claude
python run_claude.py --config config/bedrock.yaml

# Phase 3 (future)
cd agent-evolve/agent
python run_agent.py --config config/production.yaml
```

## CURRENT BLOCKERS
1. **Gemini 2.0 Access**: Verify experimental model availability
2. **Python 3.12 Compatibility**: Ensure all dependencies support Python 3.12
3. **Bedrock Permissions**: AWS IAM setup for Claude model access

## SUCCESS CRITERIA
- [ ] Python 3.12 environment operational
- [ ] Gemini 2.0 Flash generates valid code
- [ ] FizzBuzz evolution shows improvement
- [ ] Ready for Bedrock integration in Phase 2

**Next Action**: Complete Gemini integration with Python 3.12 environment.
