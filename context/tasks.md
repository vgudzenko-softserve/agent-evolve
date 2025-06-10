# AgentEvolve Task Queue

## ACTIVE: Phase 1 PoT (`pilot/`) - OpenEvolve Pattern Implementation

### 🟢 COMPLETED - Current Sprint

#### **AE-001**: OpenEvolve Pattern Implementation
**Status**: COMPLETED ✅
**Environment**: Python 3.12, OpenEvolve framework

Following the exact pattern from `openevolve/examples/function_minimization`:

```bash
agent-evolve/pilot/
├── config.yaml              # OpenEvolve configuration
├── initial_program.py        # FastAPI backend with EVOLVE-BLOCK markers
├── evaluator.py             # Multi-stage evaluation system
├── requirements.txt         # Dependencies (fastapi, uvicorn, pydantic)
└── README.md               # Documentation following OpenEvolve pattern
```

**Completed Subtasks**:
- [x] ✅ Created pilot directory structure
- [x] ✅ Implemented config.yaml with Gemini 2.0 Flash configuration
- [x] ✅ Created initial_program.py with FastAPI backend (replaces FizzBuzz)
- [x] ✅ Built evaluator.py with HTTP endpoint testing
- [x] ✅ Added requirements.txt with FastAPI dependencies
- [x] ✅ Written comprehensive README.md

---

#### **AE-002**: FastAPI Backend Evolution Task
**Status**: COMPLETED ✅
**Replaces**: FizzBuzz implementation

```python
# pilot/initial_program.py - EVOLVE-BLOCK contains:
- FastAPI app creation and configuration
- CRUD API endpoints (GET, POST, PUT, DELETE)
- Pydantic data models
- Basic error handling
- In-memory task storage
```

**Evolution Target**: Improve API structure, validation, error handling, and performance

**Completed Subtasks**:
- [x] ✅ FastAPI service with 6 REST endpoints
- [x] ✅ Pydantic models for request/response validation
- [x] ✅ Basic CRUD operations implementation
- [x] ✅ HTTP status code handling

---

#### **AE-003**: Multi-Stage HTTP Evaluator
**Status**: COMPLETED ✅

```python
# pilot/evaluator.py - Features:
- FastAPI server startup and testing
- HTTP endpoint functionality testing
- Performance measurement (response times)
- Error handling validation (404 responses)
- Multi-metric scoring system
```

**Evaluation Metrics**:
- **Functionality Score** (70%): CRUD endpoint success rates
- **Performance Score** (20%): Average response time
- **Reliability Score** (10%): Error handling accuracy

**Completed Subtasks**:
- [x] ✅ Server startup automation with timeout
- [x] ✅ HTTP endpoint testing suite
- [x] ✅ Performance benchmarking
- [x] ✅ Multi-stage evaluation (stage1 + stage2)

---

### 🔴 IMMEDIATE - Ready to Execute

#### **AE-004**: Environment Setup & First Evolution Run
**Status**: READY TO START

```bash
# Quick start commands
cd agent-evolve/pilot
pip install -r requirements.txt
pip install -e ../openevolve
export GOOGLE_API_KEY="your-gemini-key"

# Run evolution
python ../openevolve/openevolve-run.py initial_program.py evaluator.py --config config.yaml --iterations 50
```

**Subtasks**:
- [ ] Install dependencies and set up environment
- [ ] Configure Gemini API key
- [ ] Execute first evolution run (50 iterations)
- [ ] Validate evolution results and metrics

---

### 🟡 NEXT SPRINT - Phase 2 Prep (`claude/`)

#### **AE-005**: AWS Bedrock Setup
**Status**: PLANNED (after Phase 1 validation)

Following the same OpenEvolve pattern for Phase 2:
```bash
agent-evolve/claude/
├── config.yaml              # Bedrock configuration
├── initial_program.py        # Enhanced FastAPI backend
├── evaluator.py             # DeepEval integration
└── requirements.txt         # AWS Bedrock dependencies
```

---

## DEVELOPMENT ENVIRONMENT

### Phase 1 Setup (Current)
```bash
# Python 3.12 environment
conda create -n agent-evolve python=3.12
conda activate agent-evolve

# Install OpenEvolve and dependencies
cd agent-evolve
pip install -e ./openevolve
pip install -r pilot/requirements.txt

# API Configuration
export GOOGLE_API_KEY="your-gemini-key"
```

### Execution Command (Phase 1)
```bash
cd agent-evolve/pilot
python ../openevolve/openevolve-run.py initial_program.py evaluator.py --config config.yaml --iterations 50
```

## CURRENT STATUS
✅ **Implementation Complete**: All Phase 1 files created following OpenEvolve patterns
✅ **Pattern Compliance**: Exact structure from `function_minimization` example
✅ **Practical Task**: FastAPI backend evolution instead of academic problems
⏳ **Ready to Execute**: Environment setup and first evolution run

## SUCCESS CRITERIA - Phase 1
- [ ] Environment setup successful
- [ ] Initial evolution run completes (50 iterations)
- [ ] FastAPI backend functionality improves over generations
- [ ] Metrics show progression in functionality/performance scores
- [ ] Ready for Phase 2 Claude integration

**Next Action**: Execute environment setup and run first evolution cycle.
