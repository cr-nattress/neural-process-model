# Documentation Directory

This directory contains all research, design, implementation, and program documentation for the Cognitive Systems Analogy Lab (CSAL).

## Directory Structure

### `/00_Foundations`
Core theoretical foundations, principles, and frameworks that underpin the entire project.

**AI Usage:** Use for fundamental concepts, theoretical grounding, and philosophical principles. Embed these documents for high-level reasoning about project direction.

### `/01_Research`
Research papers, literature reviews, neuroscience studies, and experimental designs.

**AI Usage:** Source of scientific grounding and research methodology. Use for citation, evidence-based design decisions, and hypothesis formation.

### `/02_Design`
System architectures, cognitive module specifications, design patterns, and technical blueprints.

**AI Usage:** Primary reference for implementation planning. Use for understanding system structure, module interfaces, and architectural decisions.

### `/03_Implementation`
APIs, schemas, code specifications, decision records, and implementation guides.

**AI Usage:** Concrete technical specifications. Use for code generation, API integration, and implementation details.

### `/04_Experiments`
Experimental designs, test plans, simulation configurations, and validation methodologies.

**AI Usage:** Reference for testing strategies, benchmark definitions, and experimental protocols.

### `/05_Reports`
Progress reports, analysis results, benchmarks, and research findings.

**AI Usage:** Track project evolution, learn from past results, and inform future decisions.

### `/06_Program`
Roadmaps, milestones, governance, team roles, and project management.

**AI Usage:** Understand project timeline, priorities, and organizational structure.

## Metadata Standards

All documents should include YAML front-matter with the following fields:

```yaml
---
title: Document Title
type: [research|design|implementation|experiment|report|program]
cognitive_function: [executive|memory|creativity|emotion|learning|perception|language|social|regulation]
ai_mapping: [relevant AI component or pattern]
last_update: YYYY-MM-DD
tags: [tag1, tag2, tag3]
---
```

## AI Integration Notes

- **Embedding Strategy:** Each document type should be chunked and embedded separately for targeted retrieval
- **Semantic Search:** Use metadata fields to filter by cognitive function, AI mapping, or document type
- **Hierarchical Navigation:** Start with foundations, then research, then design, then implementation
- **Cross-References:** Documents should link to related docs across categories
