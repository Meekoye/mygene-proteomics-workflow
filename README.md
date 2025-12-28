# mygene-proteomics-workflow
A reproducible Python pipeline for proteomics data preprocessing, including UniProt protein ID to gene symbol annotation using MyGene, CPM-based normalization, and log₂ transformation for downstream quantitative analysis.
## Features

- Upload and parse proteomics CSV files
- Map UniProt protein IDs to gene symbols
- Support for organism-specific annotation (default: *Arabidopsis thaliana*)
- Counts Per Million (CPM) normalization
- Log₂ transformation for variance stabilization
- Produces analysis-ready data tables

---

## Requirements

- Python 3.7+
- Google Colab (recommended) or local Python environment

### Python dependencies
```

pandas
numpy
mygene

````

Install dependencies:
```bash
pip install pandas numpy mygene
````

---

## Input Data Format

The input file must be a **CSV file** with:

* A column named `Protein_IDs` (used as index)
* Numeric sample intensity columns
* Optional annotation columns such as:

  * `GeneID`
  * `Protein.names`
  * `Gene.names`

Example:

| Protein_IDs | Sample_1 | Sample_2 | GeneID | Protein.names |
| ----------- | -------- | -------- | ------ | ------------- |
| P12345      | 10234    | 9843     | 111    | Protein A     |

---

## Usage

### Google Colab

1. Open the notebook in Google Colab
2. Run the script
3. Upload your proteomics CSV file when prompted

### Key Steps Performed

1. Load proteomics data
2. Annotate UniProt protein IDs with gene symbols
3. Normalize sample intensities using CPM
4. Apply log₂(x + 1) transformation
5. Output a clean, annotated DataFrame

---

## Normalization Method

**Counts Per Million (CPM):**

```
CPM = (protein intensity / total sample intensity) × 1,000,000
```

Followed by:

```
log₂(CPM + 1)
```

This approach reduces sample-to-sample variation and stabilizes variance.

---

## Organism Support

The pipeline uses **MyGene** for annotation.
Default organism:

* *Arabidopsis thaliana* (NCBI Taxonomy ID: `3702`)

You can change the species by modifying:

```python
species=3702
```

---

## Output

* Annotated proteomics DataFrame
* Normalized and log₂-transformed quantitative values
* Gene symbols appended for downstream analysis

---

## Example Output Columns

* Sample_1
* Sample_2
* ...
* Gene_symbols

---

## Notes

* Not all protein IDs may map to gene symbols
* Missing mappings will result in `NaN` values
* Ensure UniProt IDs are valid and species-specific

---


