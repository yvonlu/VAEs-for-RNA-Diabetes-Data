# VAEs-for-RNA-Diabetes-Data

#Overview
This project applies dimensionality reduction techniques to analyze single-cell RNA sequencing (scRNA-seq) data from pancreatic islet cells, distinguishing between Type 2 Diabetes (T2D) patients and non-diabetic controls. The primary technique used is Variational Autoencoders (VAEs), alongside traditional methods like PCA, t-SNE, and UMAP. Our goal is to construct an informative latent space to identify gene expression patterns relevant to diabetes pathology.

#Key Contributions
Developed a robust pipeline for processing and normalizing scRNA-seq data.
Explored multiple dimensionality reduction techniques, including PCA, t-SNE, UMAP, and VAEs.
Implemented Variational Autoencoders (VAEs) to uncover meaningful latent features.
Evaluated performance using clustering metrics, such as Silhouette Score, Adjusted Rand Index (ARI), and F-Scores.
Investigated the impact of gene selection and expressivity on clustering performance.

#Data Source
Dataset: GSE81608 (obtained from GEO) containing RNA-seq data from pancreatic islet cells.
Metadata: Manually extracted and aligned using Scanpy.

#Methods
1. Data Processing
Metadata Alignment: Mapped control/T2D labels, age, and gender from external files.
Normalization: Used Scanpy’s normalize_total() to ensure uniform total gene counts per cell.
Imputation: Filled missing values via linear interpolation.
Balancing: Random sample deletion equalized T2D and control counts (final: 1302 samples).
Gene Selection: Identified genes based on variance and total expression across samples.
2. Dimensionality Reduction
PCA (Baseline) → Linear transformation to identify key variance components.
t-SNE → Nonlinear mapping for cluster visualization (failed to separate T2D/control groups).
UMAP → Improved structure and clearer separation of diabetic vs. non-diabetic samples.
VAE (scVI Library) → Learned meaningful latent features to improve clustering.
3. Clustering & Evaluation
Leiden Clustering → Applied to latent space for pattern recognition.
Performance Metrics:
Silhouette Score (Cluster tightness)
Adjusted Rand Index (ARI) (Alignment with control/T2D labels)
F-Score (Predictive power via Logistic Regression & SVM)

#Results & Findings
PCA & t-SNE failed to separate diabetic and non-diabetic groups (Silhouette Score < 0.01).
UMAP showed promise (Silhouette Score 0.31, ARI 0.21, F-score 0.72).
VAE (All Cell Types) improved latent space, but clustering was dominated by cell types rather than T2D/control status.
VAE (Single Cell Type):
Beta cells performed best (Silhouette Score 0.45, ARI 0.25, F-Score 0.84).
Alpha cells showed weaker separation.
Including only highly expressive genes improved clustering.
