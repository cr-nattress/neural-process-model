# AI Configuration

## Purpose
Configuration files, prompts, embeddings, and training resources for AI/LLM integration with the CSAL project.

## Directory Structure

### `/embeddings`
Embedding configurations and pre-computed embeddings for documentation and code.

**Contents:**
- Embedding model configurations
- Pre-computed document embeddings
- Code embeddings
- Chunking strategies
- Vector store configurations

**Models:** OpenAI text-embedding-3, Cohere, custom models

**AI Usage:** These enable semantic search across all project documentation and code.

### `/prompts`
Prompt libraries for LLM agents and tools.

**Contents:**
- System prompts for cognitive agents
- Task-specific prompts
- Few-shot examples
- Prompt templates
- Chain-of-thought patterns
- Metacognitive prompts

**AI Usage:** Reusable prompts for consistent agent behavior and reasoning patterns.

### `/training`
Training configurations and fine-tuning resources.

**Contents:**
- Fine-tuning datasets
- Training scripts
- Model configurations
- Hyperparameter settings
- Training logs

**AI Usage:** For specialized cognitive module training.

## AI Configuration Standards

### Embedding Strategy
```json
{
  "model": "text-embedding-3-large",
  "dimensions": 3072,
  "chunking": {
    "method": "semantic",
    "max_tokens": 512,
    "overlap": 50
  },
  "metadata_fields": [
    "cognitive_function",
    "brain_analogue",
    "module",
    "document_type"
  ]
}
```

### Prompt Template Format
All prompts should include:
1. Cognitive function mapping
2. Expected behavior
3. Input/output format
4. Examples
5. Constraints

### Metadata for AI Optimization
Every document/code file should be tagged with:
- `cognitive_function`: Which brain function it relates to
- `ai_mapping`: Computational equivalent
- `brain_analogue`: Biological inspiration
- `retrieval_priority`: HIGH/MEDIUM/LOW
- `embedding_strategy`: How to chunk and embed

## Vector Store Configuration

### Recommended Setup
- **Vector DB:** Pinecone or Qdrant
- **Dimensions:** 3072 (OpenAI) or 1024 (Cohere)
- **Distance Metric:** Cosine similarity
- **Namespaces:**
  - `docs_foundations`
  - `docs_research`
  - `docs_design`
  - `docs_implementation`
  - `code_modules`
  - `code_agents`

### Retrieval Strategy
1. **Hybrid search:** Combine vector similarity with metadata filters
2. **Reranking:** Use cross-encoder for final ranking
3. **Context assembly:** Hierarchical retrieval (overview → detail)
4. **Multi-query:** Generate multiple query variations for robustness
