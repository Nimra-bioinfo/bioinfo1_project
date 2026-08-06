# Comparative Target Analysis Pipeline: Automated Multi-Species Serotonin 5-HT2A Sequence Profiler

An exploratory bioinformatics project comparing the sequence metrics, structural conservation, and evolutionary variations of the Serotonin 5-HT2A receptor across species (**Human, Mouse, and Zebrafish**).

---

## Key Discoveries

* **High Evolutionary Conservation:** Human and Mouse 5-HT2A receptors share a **91.51% sequence identity** (Alignment Score: 431.0) despite ~80+ million years of evolutionary separation.
* **Length Consistency:** Both Human (*Homo sapiens*) and Mouse (*Mus musculus*) receptors consist of **471 amino acids**, while Zebrafish (*Danio rerio*) consists of **466 amino acids**.
* **Precise Point Mutations:** Identified **40 total mismatches** between Human and Mouse sequences, localized primarily in non-conserved outer regions (e.g., `Pos 2: D -> E`, `Pos 7: E -> D`, `Pos 9: T -> I`, `Pos 15: T -> P`).

---

##  Tools & Technologies Used

* **Python 3** (Core execution environment)
* **Biopython** (Data parsing, FASTA handling, and `PairwiseAligner` algorithm execution)
* **Requests** (Fetching live UniProt database entries dynamically via REST API)
* **io.StringIO** (In-memory text streaming without intermediate file storage)
* **Matplotlib** (Data visualization & sequence metric plotting)

---

##  Dataset Sources

All raw sequence data is fetched dynamically from the **UniProt Knowledgebase**:
* **Human (*Homo sapiens*):** [`P28223`](https://www.uniprot.org/uniprotkb/P28223)
* **Mouse (*Mus musculus*):** [`P35363`](https://www.uniprot.org/uniprotkb/P35363)
* **Zebrafish (*Danio rerio*):** [`Q98894`](https://www.uniprot.org/uniprotkb/Q98894)

---

##  Real-World Applications & Impact

* **Preclinical Target Validation:** Helps computational biologists quickly verify if animal models (like mouse or zebrafish) maintain the target protein structure before investing in costly lab experiments.
* **Drug Discovery Workflows:** Serves as an automated data-ingestion and pairwise alignment module that can be integrated into downstream machine learning pipelines for virtual screening, molecular docking, and binding affinity prediction.
* **Cross-Species Pharmacodynamics:** Quantifies amino acid mismatches in active pockets to evaluate whether novel psychotherapeutic compounds will exhibit similar binding kinetics across species.

---

#  Project Purpose, Research Questions & Critical Analysis

##  1. Key Research Questions & Mindset

Before executing the computational workflow, several key research, biological, and technical questions were addressed:

> **Q1: Why was this project conducted, and what is its real-world practical value?**
> * **Answer:** The primary objective of this project is to perform a comparative bioinformatics analysis on the **Serotonin 5-HT2A Receptor** across three key biological species (*Homo sapiens*, *Mus musculus*, and *Danio rerio*). 
> 
> In modern biomedical research, testing new drugs directly on humans is ethically and practically impossible during the early stages. Scientists rely heavily on **model organisms** like mice and zebrafish. By analyzing and comparing the amino acid sequences of this receptor, we can determine how structurally conserved the target protein is across species, validating whether these animals serve as accurate biological models for human neurological diseases.

> **Q2: How does this pipeline help in Pharmaceutical Drug Discovery (Pharmacology)?**
> * **Answer:** The 5-HT2A receptor is the primary target for **atypical antipsychotics** (used to treat schizophrenia and depression) as well as **psychedelic therapeutics**. Knowing that the Human and Mouse receptors have high sequence similarity and identical length (471 amino acids) helps pharmacologists predict whether a drug tested on a mouse model will bind similarly to the human receptor binding pocket.

> **Q3: What is the benefit of automating sequence retrieval instead of doing it manually?**
> * **Answer:** Manual retrieval of FASTA files from web databases is slow, prone to human error, and hard to scale. By engineering an automated Python pipeline using the UniProt REST API:
>   1. **Scalability:** The pipeline can be scaled instantly from 3 species to 300+ species by simply modifying a single dictionary.
>   2. **Reproducibility:** Any researcher globally can run the exact same notebook and dynamically pull the latest, most up-to-date reference sequences directly into memory.

> **Q4: Why use Global Pairwise Alignment (Needleman-Wunsch) instead of simple string comparison?**
> * **Answer:** Simple string comparison breaks down when sequences vary in length or contain insertions/deletions (indels). Biopython's `PairwiseAligner` executes global alignment algorithms to optimal score pathways, ensuring gaps are appropriately scored while accurately calculating percentage identity across non-identical sequence lengths (e.g., Human vs. Zebrafish).

> **Q5: What is the biological significance of identifying exact point mismatches (e.g., Pos 2: D -> E)?**
> * **Answer:** The primary goal of comparing Human and Mouse 5-HT2A sequences is to evaluate functional conservations and structural identity for preclinical drug screening applications.
 
> Identifying exact point substitutions provides crucial sequence-level insights:
>   - **Charge Conservation:** Swapping Aspartic Acid for Glutamic Acid (`Pos 2: D -> E`) maintains overall negative charge, preserving local ionic interactions.
>   - **Structural Rigidity:** Swapping Threonine for Proline (`Pos 15: T -> P`) introduces conformational rigidity, as Proline typically alters local peptide backbone flexibility.
>   - **Overall Conservation:** Out of 471 amino acids, only 40 variations were detected (91.51% identity). The overall high sequence conservation indicates that Mouse 5-HT2A serves as a highly reliable structural surrogate for testing human-targeted therapeutics.

---

## 2. Methodological Decisions & Code Architecture

The repository is organized into modular scripts for clean execution and maintainability:

```text
5HT2A-Target-Profiler/
│
├── README.md                   # Full Documentation & Analytical Report
├── requirements.txt            # Python dependencies (biopython, requests, matplotlib)
│
├── 01_sequence_lengths.py      # Module 1: UniProt fetcher & sequence length analyzer
└── 02_pairwise_alignment.py   # Module 2: Pairwise alignment & point mutation mapper
```

### A. Modular Breakdown
* **`01_sequence_lengths.py`:** Focuses on dynamic ingestion, in-memory buffering using `io.StringIO`, and cross-species sequence length distribution profiling.
* **`02_pairwise_alignment.py`:** Implements Biopython's `PairwiseAligner` to calculate normalized percent identity and extract position-specific point mutations.

##  Conclusion & Future Directions

This project demonstrates an end-to-end bioinformatics workflow combining raw sequence analysis, pairwise sequence alignment, mutation mapping, and rich scientific documentation. Future iterations will incorporate:
1. Multi-sequence alignments (MSA) using Clustal Omega / MUSCLE.
2. 3D protein structure comparison (PDB files) to map mutated positions directly onto the binding pocket.

##  How to Execute the Pipeline

Follow these simple steps to run the pipeline locally on your machine:

### 1. Clone the Repository
```bash
git clone https://github.com/Nimra-bioinfo/bioinfo1_project.git
cd bioinfo1_project
```

### 2. Install Required Dependencies
```bash
pip install biopython requests matplotlib
```

### 3. Run Pipeline Modules

* **Execute Sequence Length Analysis:**
  ```bash
  python 01_sequence_lengths.py
  ```

* **Execute Global Pairwise Alignment & Mutation Tracker:**
  ```bash
  python 02_pairwise_alignment.py
  ```