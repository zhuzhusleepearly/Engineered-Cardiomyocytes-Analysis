## Question 1 How pure are your engineered cardiomyocytes? ##
The pySCN package was used to validate the purity of cardiomyocyte (CM) cells from Stone’s subsampled 5000 cells data. pySCN was trained with a reference dataset from Tabula Muris. 
From Figure 1, we can see that the trained model in cell typing performed well with high precision. 184 cells in the dataset were recognized as CM cells with major enrichment in the batch 6 cell (day 14) population (Fig. 2). A large number of cells in Stone et al. 's study are random cells which are not recognized by pySCN. This is sensible as the cells were analyzed in different time points and the majority of the cells are still in less differentiated transition or undifferentiated states. By performing the comparison between the Stone’s engineered CMs and the reference data, we can conclude that the engineered cardiomyocytes have relatively poor purity. 


Figure 1. Trained Model Reliability


Figure 2. Heatmap of Cell Types in Different Batches From the Reference Dataset. Cardiac Muscle Cell Mainly Expressed in Batch 6 (day 14). Cardiac Muscle Cell Counts: 184

Figure 3. UMAP of Cardiac Muscle Cells, Fibroblast, and Smooth Muscle Cells

	In terms of exploring the dataset, dimensionality reduction of Stone’s engineered CMs with uniform manifold approximation and projection (UMAP) revealed that clusters are formed for certain cell types (Fig.3). 

## Question 2 How mature are your engineered cardiomyocytes? ##
The CM cells were selected from the previous procedure. The second step is to determine the temporal maturity of the CM cells. Using the entropy method described in Kannan et al’s paper and the featured CM maturation TF (transcription factor) markers from Padula et al’s paper (2021), 
Cells with higher maturity tend to have lower entropy values (Figure 4). The engineered CM cells are relatively less mature with the majority of cells enriched at early time points, e14, e18 and p0 stages. Only a few cells are more mature as can be seen from Figure 6. 


Figure 4. Shannon Entropy of Each Timepoint in Kannan’s Reference Dataset


Figure 6. Shannon Entropy of Each Timepoint in Stone’s Engineered CM Cells. Batch 3, 4, 5 and 6 indicate day 2, 3, 7 and 14, respectively. Timepoint values were assigned depending on the developmental time scale (see Table 1 for reference).

## Question 3 What genetic alterations could improve your engineered cardiomyocytes? How well do CellOracle’s predicted fold changes correspond to what would actually happen? ##
1) CellOracle was trained with Kannan’s perinatal reference dataset. 18 CM characteristic transcription factor-targets networks (Padula et al, 2021) were added to the Oracle object for CM cells’ GRN activation.

2) Then we showcase the network perturbation on the evaluation dataset from Wu et al. by knocking out the Prdm16 expression. The inner product score was used as an indicator of change in cell state. A positive value indicates change in a similar direction whereas a negative value indicates opposing cell state transfer. Our results (Figures 6, 7 & 8) show that with later CM state (larger pseudotime value), CM cells are more sensitive to the treatment of Prdm16 knockout, as signified by the lower inner product over increased pseudotime value. This is consistent with the wet lab result conducted by Wu et al (2022), where Prdm16 is required to maintain cardiomyocyte identity for left ventricle. 

3) We only utilized the default base gene regulatory network inserted in the CellOracle package.

4) As shown in Figure 9, we ranked the usefulness of three TFs (Foxo1, Clock, Prdm1
) by the average inner product scores from high to low. The most useful TF is Foxo1 indicated by the lowest inner product, meaning Foxo1 is required. This observation contradicts the previous study held by Uosaki et al (2015, Transcriptional landscape of Cardiomyocyte Maturation), where Foxo1 expression is decreased in neonate-adult CM cells, suggesting that low level Foxo1 is required for CM maturation. This may be explained by the different roles of Foxo1 at different maturation stages, where Foxo1 is required for early CM lineage commitment (as the majority of the mouse CMs are in early developmental stages) but should be decreased when CM cells undergo later stage maturation. Another rationale is that Uosaki et al’s study exploits human cells whereas the tested dataset is from mouse cells. Discrepancy of the roles of TFs in CM development across species is possible. Since the scores are all negative, these three TFs are all beneficial to drive the maturation of CM cells. We only tested the perturbation of three TFs due to lack of computational power. All TFs in the dataset would be tested for knockout and overexpression simulation whenever there is enough computational power.

Figure 6. Quiver Plot for Simulated Cell Identity Shift Vector. Arrows indicate the direction in cell state change led by Prdm16 knockout.

Figure 7. Calculated Gradient of Pseudotime (Development Flow). Red color indicates high pseudotime value while blue color indicates low pseudotime value. High pseudotime values indicate later differentiation stages relative to others. Arrows indicate developmental flow of the cells

Figure 8. Visualization of Inner Product Score (Perturb Simulation * Development Flow) by Prdm16 knockout. The lower the inner product score brought by Prdm16 knockout, the more highly the cells deviate from their previous identity.

Figure 9. Genes Knocked Out vs. Inner Product Scores

## Question 4 How can your computational methods be translated to help engineer human cardiomyocytes? ##
Same assessments and TF screening methods from question 1 to 3 were applied to human iPSCs. However, initially, we performed gene mapping for human cells on mouse cells as the two species have different names for orthologs. 
As shown in Figure 13, since the scores are all positive, knockout of each of the four TFs (Foxo1, Prdm1, Cux1, Ctcf) cannot provide enough improvement for the maturity of CMs, suggesting that they should be absent in order to support CM cells maturation. This result for Foxo1 is especially consistent with the previous result obtained by Uosaki et al (2015, Transcriptional landscape of Cardiomyocyte Maturation). Foxo1 was found to be decreased in expression in neonatal adult CM cells.


Figure 10. Cell typing of orthologs-converted human engineered cardiomyocytes from Giacomelli et al by pySCN. Cardiomyocyte number = 116. Similar to the mouse engineered CM cells dataset, the majority of the cells are not discernible by pySCN, suggesting the transitioning cell state.

Figure 11. Stage composition for engineered human CM cells. The majority of the cells are at postnatal day 22 stage.



Figure 12. UMAP of engineered human CM cells from Giacomelli et al. Random cells 


Figure 13. Genes knockout vs. inner product scores For human engineered CM cells.
