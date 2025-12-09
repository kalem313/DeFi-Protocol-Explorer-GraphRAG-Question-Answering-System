# DeFi Protocol Explorer: GraphRAG Question Answering System

This repository contains the full Proof-of-Concept (PoC) development for a Question Answering (QA) system designed to query the Decentralized Finance (DeFi) ecosystem. The project demonstrates the **Graph Retrieval-Augmented Generation (GraphRAG)** paradigm, leveraging a structured Knowledge Graph (KG) to provide *verifiable, hallucination-free answers*.

---

## Project Overview

The **DeFi Protocol Explorer** addresses the problem of data fragmentation in the crypto sector by structuring data about protocols, blockchains, and their relationships (audits, partnerships, migration paths) into an ontological model.

The system's core value is delivering **Grounded AI** — ensuring that all answers are directly sourced from the Knowledge Graph.

---

## Core Architecture: GraphRAG

The system operates on a two-stage pipeline:

### **1. NL-to-SPARQL Translation (LLM Simulation)**
Natural Language questions are mapped to structured SPARQL queries.  
In this PoC, this function is simulated through **Python Rule-Based Logic and Regex**, illustrating current architectural trade-offs.

### **2. KG Lookup (Grounded Fact Retrieval)**
The generated SPARQL query is executed against a **Virtuoso graph database**, ensuring every answer is a *verifiable fact* from the Knowledge Graph.

---

## Technical Implementation Details

### **1. Knowledge Graph Schema (Assignment 2)**

- **Format:** RDF/OWL Ontology (Turtle format: `defi_schema.ttl`)
- **Core Entities:**  
  `Protocol`, `Blockchain`, `Organization` (Auditors, VCs), `Token`
- **Key Relationships:**  
  - `DEPLOYED_ON`  
  - `AUDITED_BY`  
  - `HAS_TVL` (*xsd:decimal*)  
  - `MIGRATED_TO` *(critical for tracking blockchain migration)*

---

### **2. KG Population Pipeline (Assignment 3)**

A major component was designing and validating the automated ingestion pipeline.

- **Methodology:**  
  Developed an **LLM-based Entity Extractor** and an **LLM-as-a-Judge** evaluation system.
- **Validation:**  
  Measured **Precision** and **Recall** on a custom evaluation dataset.
- **LLM API Usage:**  
  Required for complex reasoning, extraction, and validation capabilities.

---

### **3. QA System Evaluation (Assignment 4)**

The evaluation quantified the system’s real-world reliability and provided a roadmap for scaling.

| Evaluation Metric | Result | Strategic Implication |
|-------------------|--------|------------------------|
| **Expected Accuracy (Core Logic)** | **100%** | Confirms schema integrity and correctness of core query logic. |
| **Adversarial Robustness (Simulation)** | **85%** | The 15% fragility in translation motivates migrating to full LLM-based translation. |

---

## Future Roadmap

The transition toward a production-grade system focuses on the following enhancements:

### **• LLM Integration**
Replace the Rule-Based NL-to-SPARQL Translator with a dedicated LLM for significantly improved flexibility and robustness.

### **• Multi-Hop Reasoning**
Extend the system to support complex analytical queries spanning multiple relationships in the graph.

### **• Strategic Data Monitoring**
Enable and monitor properties like `MIGRATED_TO` to track protocol migrations in real time.

### **• Answer Synthesis**
Implement an LLM post-processor to convert raw KG outputs (URIs) into polished, natural-language answers.

---

