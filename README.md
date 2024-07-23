# Entanglement in the AlphaFold predicted structures
Currently, our data is available only for the human proteome. More organisms will be added soon.

We are finalizing the data, and the repository structure will be changed and reorganized in the future.

Data in this repository involves multiple quality control steps for structures and entanglement. Our procedure is as follows:


1. **Selecting High-Confidence Proteins:**
* We select only those UniProt entries that have a global average pLDDT (predicted Local Distance Difference Test) score of 70 or higher.

2. **Processing Crossing Residues to Handle Slipknots:**
* We process the crossing residues to manage slipknots in the list of crossing residues. We provide three datasets that differ in how slipknots are handled:

   a. **All Slipknots Included** (`_all_slipknots_*.pkl`): Slipknots identified in the crossing residues list are not removed.

   b. **Pure Slipknots Removed** (`_no_pure_slipknots_*.pkl`):
  * We remove only pure slipknots. A pure slipknot is defined as a crossing residues list where, after chirality reduction, all crossing residues are canceled out.
  * For example, consider a loop closed by contact `[100, 200]` and N-terminal crossing residues `[20, -35]`. This means the N-terminal does not thread around the loop but only pierces the surface bounded by the loop and then returns
  * For mixed-slipknot: `[20, -35, 45]`, the chirality is `[+,-,+]` after reduction resulting `[+]` we will retain the original crossings: `[20, -35, 45]`
  
   c. **All Slipknots Removed** (`_no_slipknots_*.pkl`):
  * We check the chirality of crossing residues for each terminus and remove all slipknots.
  * As the example above, pure slipknot will be completely removed, mixed slipknots will retain `[20]`

3. Retaining High-Confidence Crossing Residues:
   * We apply a procedure to process the crossing residues. This procedure involves iterating through the list of crossing residues, starting from the loop indices and moving away sequentially, including residues as long as their confidence score is 70 or higher. The procedure stops as soon as it encounters a residue with a confidence score below the threshold. This ensures that only residues with sufficiently high confidence scores are retained.
   

# Available Datasets

We provide various datasets for each organism depending on the research question. Currently, for the human proteome, the datasets are:

1. `data/AF_Human_all_slipknots_v1.pkl`: Includes all slipknots without checking their presence in the list of crossing residues.
2. `data/AF_Human_no_pure_slipknots_v1.pkl`: Removes only pure slipknots and does not modify mixed slipknots.
3. `data/AF_Human_no_slipknots_v1.pkl`: Does not contain any slipknots.


These datasets are tailored to facilitate specific analyses related to protein entanglement and their structural properties.

# Contributors:
1. Quyen Vu
2. Ian Sitarik
3. Ed O'Brien