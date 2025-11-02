# Data

## Purpose
Storage for memory structures, datasets, experimental results, and training data.

## Directory Structure

### `/memory`
Persistent memory stores for cognitive agents.

**Contents:**
- Episodic memory databases (vector stores)
- Semantic memory (knowledge graphs)
- Procedural memory (learned patterns)
- Working memory snapshots
- Emotional memory associations

**Format:** Primarily vector embeddings, graph databases (Neo4j), and structured JSON/SQL.

**AI Usage:** These are active data stores that agents read from and write to during operation.

### `/datasets`
Training and evaluation datasets.

**Contents:**
- Cognitive task datasets
- Behavioral training data
- Perception training sets
- Language corpora
- Benchmark task data

**Format:** CSV, JSON, Parquet, HDF5 for large arrays.

**AI Usage:** Used for training cognitive modules and validating performance.

### `/results`
Experimental results, logs, and analysis outputs.

**Contents:**
- Experiment logs
- Performance metrics
- Benchmark results
- Visualization outputs
- Analysis reports

**Format:** JSON logs, CSV metrics, PNG/SVG visualizations.

**AI Usage:** For analysis, reporting, and tracking improvement over time.

## Data Standards

### Metadata Requirements
All datasets should include a metadata file:

```yaml
---
name: Dataset Name
type: [episodic|semantic|procedural|training|benchmark]
cognitive_function: [relevant function]
size: [record count]
format: [csv|json|parquet|embeddings]
created: YYYY-MM-DD
description: |
  Detailed description of dataset contents and purpose
schema:
  - field_name: type (description)
---
```

### Privacy & Ethics
- No personally identifiable information (PII)
- Synthetic data preferred for sensitive domains
- Document data provenance
- Include data use restrictions

## AI Tool Integration
- Vector stores should be indexed for semantic search
- Include embedding model specifications
- Document chunking and retrieval strategies
- Maintain version history for datasets
