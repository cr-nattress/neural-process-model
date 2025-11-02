# Source Code

## Purpose
This directory contains all implementation code for the Cognitive Systems Analogy Lab, organized by cognitive function and system layer.

## Directory Structure

### `/agents`
Multi-agent implementations inspired by brain networks and specialized cognitive functions.

**Contents:**
- Executive agents (planning, reasoning, decision-making)
- Memory agents (storage, retrieval, consolidation)
- Perceptual agents (input processing, pattern recognition)
- Creative agents (divergent thinking, recombination)
- Social agents (theory of mind, cooperation)
- Meta-cognitive agents (self-monitoring, reflection)

**AI Usage:** Each agent should be self-documented with clear interfaces and cognitive function mappings.

### `/modules`
Reusable cognitive modules implementing specific brain-inspired functions.

**Contents:**
- Working memory cache
- Attention controllers
- Emotion simulators
- Reward systems
- Pattern recognizers
- Prediction engines
- Memory consolidators

**AI Usage:** Modules should be composable and well-tested, with clear API contracts.

### `/api`
API layer for external interaction and inter-module communication.

**Contents:**
- REST API endpoints
- GraphQL schemas
- WebSocket handlers
- Message queues
- Service orchestration

**AI Usage:** APIs should follow OpenAPI specifications for automatic documentation.

### `/simulation`
Simulation environments for testing cognitive behaviors and emergent properties.

**Contents:**
- Cognitive task simulations
- Multi-agent environments
- Benchmark tasks
- Visualization tools
- Monitoring dashboards

**AI Usage:** Simulations should be reproducible with configurable parameters.

## Code Standards

### Language Conventions
- **Python:** PEP 8, type hints, docstrings
- **TypeScript:** ESLint, strict mode, JSDoc comments

### Documentation Requirements
Every module/agent must include:
1. Cognitive function mapping (which brain region/network)
2. Input/output specifications
3. Dependencies
4. Usage examples
5. Test coverage

### Metadata in Code
Use decorators/annotations to mark cognitive functions:

```python
@cognitive_module(
    brain_analogue="dorsolateral_prefrontal_cortex",
    function="working_memory",
    inputs=["sensory_data", "context"],
    outputs=["retained_info"]
)
class WorkingMemoryCache:
    ...
```

## AI Tool Integration
- All code should be compatible with LLM code analysis
- Include metadata for embedding and semantic search
- Use clear naming conventions
- Document brain-inspired design patterns
