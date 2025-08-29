# PrimeKG\_Testing

Seminar notebooks for exploring and testing workflows with **PrimeKG** (a multimodal precision-medicine knowledge graph).
This repo contains small, reproducible case studies that mirror examples from the PrimeKG paper, adapted for hands-on learning.

---

## Objectives

* ⚙️ **Load & inspect** the `kg.csv` giant component of PrimeKG.
* 🧭 **Trace mechanisms** across diseases, proteins/genes, pathways, and drugs.
* 🔁 **Replicate case studies** (Autism; Hurler syndrome; COVID-19 → Baricitinib).
* 🧪 **Test simple network analyses** (shortest paths, ego-subgraphs, lightweight permutation checks).

---

## What’s inside

```
PrimeKG_Testing/
├─ notebooks/
│  ├─ autism.ipynb  (From : PrimeKG Repository Original)
│  ├─ PrimeKG_Autism_Case_Study.ipynb
│  ├─ PrimeKG_Hurler_Syndrome_Case_Study.ipynb
│  └─ PrimeKG_COVID19_Baricitinib_Case_Study.ipynb
├─ data/
│  └─ kg.csv               # <- put PrimeKG CSV here (gitignored)
├─ .gitignore
└─ README.md
```

> **Note:** Place `kg.csv` in `data/` (or update `KG_PATH` inside each notebook).

---

## Requirements

* Python ≥ 3.9
* JupyterLab / Jupyter Notebook
* Packages: `pandas`, `networkx`, `matplotlib`, `numpy` (optional), `ipykernel`

**Quick install (pip):**

```bash
python -m venv .venv
source .venv/bin/activate           # Windows: .venv\Scripts\activate
pip install jupyter pandas networkx matplotlib numpy
python -m ipykernel install --user --name primekg-testing
```

---

## Data

* **PrimeKG** is distributed as a single CSV of triplets (source, relation, target) with rich metadata.
* The notebooks assume the following columns exist (names used by our examples):

  * `x_name`, `x_type`, `relation`, `y_name`, `y_type`
* Download the PrimeKG `kg.csv` (giant component) and save it to `data/kg.csv`.
  (If your file has different column names, adjust the notebook selectors accordingly.)

---

## Notebooks Overview

### 1) Autism Case Study

* Mirrors the paper’s autism analysis at a high level.
* Filters disease nodes, inspects connected phenotypes/proteins/pathways, and visualizes subgraphs.
* Good starting point for graph loading, filtering, and basic exploration.

### 2) Hurler Syndrome Case Study

* Focused on **MPS I (Hurler syndrome)**; explores known treatments (e.g., enzyme replacement therapy) and related biology.
* Builds a small ego-subgraph and surfaces candidate drug/disease links for discussion.

### 3) COVID-19 → Baricitinib Case Study

* Searches for **COVID-19** nodes and the drug **Baricitinib**.
* Computes shortest path(s), builds a focused subgraph, and highlights key proteins often discussed in mechanisms (e.g., **AAK1, GAK, JAK1/2**) and pathways (endocytosis, cytokine signaling).
* Includes a **mini permutation test** comparing the observed distance (COVID ↔ Baricitinib) to random diseases (lightweight, seminar-friendly).

---

## How to run

1. **Clone & set up**

   ```bash
   git clone https://github.com/RoshanRajShah/PrimeKG_Testing.git
   cd PrimeKG_Testing
   ```
2. **Add data**

   * Put `kg.csv` at `data/kg.csv`.
3. **Launch notebooks**

   ```bash
   jupyter lab   # or jupyter notebook
   ```
4. **Open any notebook in `notebooks/`**

   * If needed, edit `KG_PATH` near the top (e.g., `"data/kg.csv"`).
   * Run cells top-to-bottom.

---

## Reproducibility & Performance Tips

* **Memory:** PrimeKG is large. If you hit memory limits:

  * Downsample early (e.g., filter to relevant node/edge types before constructing a full `networkx` graph).
  * Use smaller **ego subgraphs** (reduce `EGO_RADIUS`) or limit visualization.
* **CSV quirks:** If you see CSV parse errors (e.g., due to embedded commas/quotes), try:

  ```python
  pd.read_csv("data/kg.csv", engine="python")
  ```
* **Naming & synonyms:** Disease/drug names vary across ontologies.

  * Use **lower-case contains** matches first; then refine to MONDO/Orphanet/DrugBank IDs if necessary.
  * If your `kg.csv` includes IDs, consider mapping names ↔ IDs to be explicit.
* **Path searches:** If `cutoff=6` finds no path, increase it cautiously and/or widen your keyword set.

---

## Roadmap (nice-to-haves)

* Add **robust entity resolution** (MONDO/Orphanet/UMLS) for disease matching.
* Generalize **permutation tests** and significance reporting.
* Export **static figures** for seminar slides.
* Optional: **DuckDB** loaders and queries for speed/scale.

---

## Citations

If this repository helped your seminar or project, please cite the PrimeKG paper:

* **Chandak, Huang, Zitnik (2023)**. *PrimeKG: A multimodal precision-medicine knowledge graph.* Scientific Data 10:67.
  DOI: 10.1038/s41597-023-01960-3

Drug-repurposing context discussed in the COVID-19 notebook draws on:

* **Richardson et al. (2020)**. *Baricitinib as potential treatment for 2019-nCoV acute respiratory disease.* The Lancet 395\:e30–e31.

---

## License

* Code and notebooks in this repo: No Liscense.
* **Data:** Original PrimeKG’s license/terms apply to the CSV — please follow the dataset’s usage conditions.

---

## Disclaimer

These notebooks are for **educational and research demonstration** purposes only.
They do **not** constitute medical advice or clinical validation.

---

## Acknowledgments

* Thanks to the PrimeKG authors and maintainers for providing a unified, research-ready resource for precision medicine.
