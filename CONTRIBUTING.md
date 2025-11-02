# Contributing to CSAL

Thank you for your interest in contributing to the Cognitive Systems Analogy Lab! This document provides guidelines for contributing to the project.

---

## 🎯 Ways to Contribute

### 1. Research & Literature Review
- Add neuroscience papers to the research directory
- Summarize cognitive psychology studies
- Identify new brain-AI mappings
- Validate biological benchmarks

### 2. Code & Implementation
- Implement cognitive modules
- Write tests
- Optimize performance
- Fix bugs

### 3. Documentation
- Improve existing docs
- Add examples and tutorials
- Create diagrams and visualizations
- Write blog posts

### 4. Experiment Design
- Design validation experiments
- Run benchmarks
- Analyze results
- Document findings

### 5. Ethics & Safety
- Review ethical implications
- Propose safety mechanisms
- Identify risks
- Suggest mitigations

---

## 🚀 Getting Started

### Prerequisites

1. **Read Core Documents:**
   - [Research Charter](docs/00_Foundations/research-charter.md)
   - [Cognitive Systems Framework](docs/00_Foundations/cognitive-systems-framework.md)
   - [Ethics & Safety Whitepaper](docs/00_Foundations/ethics-safety-whitepaper.md)

2. **Set Up Environment:**
   ```bash
   git clone https://github.com/[username]/neural-process-model.git
   cd neural-process-model
   pip install -r requirements.txt
   ```

3. **Check the Roadmap:**
   - Review [current milestones](docs/06_Program/roadmap-milestones.md)
   - Check [open issues](../../issues)

---

## 📝 Contribution Process

### For Code Contributions

1. **Find or Create an Issue**
   - Check existing issues
   - Create a new issue describing your proposed change
   - Wait for discussion and approval

2. **Fork and Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Write Code**
   - Follow code standards (see below)
   - Include docstrings and comments
   - Add type hints (Python)

4. **Write Tests**
   - Unit tests for all functions
   - Integration tests for module interactions
   - Aim for >80% coverage

5. **Update Documentation**
   - Update relevant docs
   - Add examples if applicable
   - Update project manifest if needed

6. **Submit Pull Request**
   - Clear description of changes
   - Link to related issue
   - Include test results

### For Documentation Contributions

1. **Identify Gap**
   - Missing documentation
   - Unclear explanations
   - Outdated information

2. **Create or Update Docs**
   - Follow documentation standards (see below)
   - Include YAML front-matter
   - Use clear, accessible language

3. **Submit Pull Request**
   - Describe what you've added/changed
   - Explain why it's needed

---

## 📋 Standards & Guidelines

### Code Standards

#### Python
- **Style:** PEP 8
- **Type Hints:** Required for all functions
- **Docstrings:** Google style

```python
from typing import List, Optional

def embed_text(text: str, model: str = "text-embedding-3-large") -> List[float]:
    """
    Convert text to semantic embedding.

    Args:
        text: Input text to embed
        model: Embedding model name

    Returns:
        List of embedding values

    Raises:
        ValueError: If text is empty
    """
    if not text:
        raise ValueError("Text cannot be empty")

    # Implementation...
    return embedding
```

#### TypeScript
- **Style:** ESLint with strict mode
- **Comments:** JSDoc

### Documentation Standards

#### Markdown Files
All documentation should include YAML front-matter:

```yaml
---
title: Document Title
type: [foundation|research|design|implementation|experiment|report|program]
cognitive_function: [relevant function]
ai_mapping: [AI equivalent]
last_update: YYYY-MM-DD
tags: [tag1, tag2]
---
```

#### Structure
- Clear headings (H1 for title, H2 for sections)
- Concise paragraphs
- Code examples where relevant
- Links to related documents

### Cognitive Module Standards

Every cognitive module must include:

1. **Metadata Decorator**
```python
@cognitive_module(
    brain_analogue="hippocampus",
    cognitive_function="episodic_memory",
    inputs=["experiences", "context"],
    outputs=["memories"],
    version="1.0.0"
)
class EpisodicMemory:
    ...
```

2. **Clear Interface**
- Well-defined input/output types
- Error handling
- Configuration options

3. **Tests**
- Unit tests (>80% coverage)
- Integration tests
- Performance benchmarks
- Biological comparison tests

4. **Documentation**
- Module README
- API documentation
- Usage examples
- Design rationale

---

## 🧪 Testing Requirements

### Test Types

1. **Unit Tests**
   - Test individual functions in isolation
   - Use pytest
   - Mock external dependencies

2. **Integration Tests**
   - Test module interactions
   - Test data flow
   - Verify cognitive loops

3. **Performance Tests**
   - Benchmark latency
   - Measure throughput
   - Track memory usage

4. **Biological Validation**
   - Compare to brain performance
   - Run cognitive task benchmarks
   - Document differences

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src --cov-report=html

# Run specific test file
pytest tests/test_working_memory.py

# Run performance benchmarks
pytest tests/benchmarks/ --benchmark-only
```

---

## 🔍 Code Review Process

All contributions go through code review:

1. **Automated Checks**
   - Linting (flake8, pylint)
   - Type checking (mypy)
   - Tests (pytest)
   - Coverage (>80% required)

2. **Human Review**
   - Code quality
   - Design consistency
   - Documentation completeness
   - Alignment with CSAL principles

3. **Ethics Review** (for new modules)
   - Safety implications
   - Privacy concerns
   - Potential for misuse
   - Alignment with ethical guidelines

---

## 🏷️ Commit Message Guidelines

Use conventional commits format:

```
type(scope): brief description

Longer explanation if needed

Fixes #123
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `test`: Tests
- `refactor`: Code refactoring
- `perf`: Performance improvement
- `chore`: Maintenance

**Examples:**
```
feat(memory): implement episodic memory retrieval

Add semantic search functionality to episodic memory module.
Includes context filtering and pattern completion.

Fixes #45
```

```
docs(design): add cognitive architecture diagrams

Include Mermaid diagrams for system architecture and
data flow visualization.
```

---

## 🎨 Documentation Contributions

### Adding Research Papers

1. Create file in `docs/01_Research/`
2. Include metadata:
   - Authors, year, publication
   - Brain region/function studied
   - Key findings
   - Relevance to CSAL
   - AI implications

### Adding Module Specifications

1. Use template from `docs/02_Design/cognitive-module-specifications.md`
2. Include all required sections
3. Provide code examples
4. Link to relevant research

### Adding Experiments

1. Copy `docs/04_Experiments/experiment-template.md`
2. Fill in all sections
3. Include expected outcomes
4. Document methodology clearly

---

## 🤝 Community Guidelines

### Code of Conduct

- Be respectful and inclusive
- Welcome newcomers
- Provide constructive feedback
- Assume good intentions
- Focus on the science and engineering

### Communication Channels

- **GitHub Issues:** Bug reports, feature requests
- **GitHub Discussions:** Questions, ideas, general discussion
- **Pull Requests:** Code and documentation contributions

---

## 🏆 Recognition

Contributors will be:
- Listed in project documentation
- Credited in publications
- Acknowledged in release notes

Significant contributors may be invited to:
- Join the core team
- Co-author papers
- Participate in governance

---

## ❓ Questions?

- Check the [documentation](docs/)
- Search [existing issues](../../issues)
- Open a [discussion](../../discussions)
- Ask in your PR/issue

---

## 📚 Resources for Contributors

### Neuroscience
- [Neuroscience textbooks and resources]
- [Brain imaging databases]
- [Cognitive psychology benchmarks]

### AI/ML
- [LangChain documentation]
- [Vector database tutorials]
- [Reinforcement learning resources]

### Project-Specific
- [Design patterns](docs/02_Design/)
- [Module specifications](docs/02_Design/cognitive-module-specifications.md)
- [Experiment templates](docs/04_Experiments/)

---

Thank you for contributing to CSAL! Together we're building the future of cognitive AI. 🧠✨

---

**Last Updated:** 2025-11-01
**Version:** 1.0
