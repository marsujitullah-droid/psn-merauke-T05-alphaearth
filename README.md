# AlphaEarth Embeddings vs Sentinel-2 Spectral Features in the Merauke PSN Area (T05)

Code and data for the study *"AlphaEarth Foundation-Model Embeddings versus Sentinel-2 Spectral Features for Land-Cover Mapping with Limited Labels and Cross-Region Transfer in the Merauke National Strategic Project, Indonesia"*.

> **Ringkasan (ID):** Repositori ini berisi notebook, dataset sampel, dan tabel hasil untuk perbandingan embedding AlphaEarth Foundations dengan fitur Sentinel-2 (tahunan dan musiman) pada pemetaan tutupan lahan dengan label terbatas, transfer antarblok, dan klasterisasi tanpa label di Blok C dan D kawasan PSN Merauke. Semua tabel dan gambar tersedia dalam versi Indonesia (_ID) dan Inggris (_EN).

## Study design

| Item | Value |
|---|---|
| Study area | Blocks C and D (20 × 20 km, ranks 3–4 in 2024–2025 Hansen loss), Merauke Regency |
| Feature sets | S2-annual (16), S2-seasonal (32), AlphaEarth annual embedding (64), AE + S2-seasonal (96) |
| Labels | Consensus of Hansen GFC, RADD, JRC TMF, ESA WorldCover, JRC GSW (no field survey) |
| E1 | Label efficiency in Block C: 5–all points/class × 10 repeats; kNN, logistic regression, RF |
| E2 | Cross-block transfer C → D and D → C; exact McNemar |
| E3 | Label-free k-means (ARI, NMI) and t-SNE |

## Main results

Embedding year 2025; four classes (forest, savanna/shrub/grass, wetland, cleared land 2024–2025); 500 points/class/block.

| Macro-F1 (Block C, mean of 10 repeats) | kNN, 5/class | RF, 5/class | kNN, all | RF, all |
|---|---|---|---|---|
| S2-annual | 0.806 | 0.798 | 0.843 | 0.846 |
| S2-seasonal | 0.795 | 0.821 | 0.912 | 0.908 |
| **AlphaEarth** | **0.908** | **0.901** | **0.947** | 0.932 |
| AE + S2-seasonal | 0.905 | 0.897 | 0.939 | **0.940** |

- Sentinel-2 features never reached AlphaEarth's F1 at 10 points/class, even with 250 points/class (> 25× label saving).
- Cross-block transfer (RF, D → C): AlphaEarth 0.885 vs S2-seasonal 0.677; AlphaEarth better in 5 of 6 direction–algorithm combinations (exception: logistic regression C → D).
- Cleared-land F1 after transfer C → D (RF): 0.919 (AE) vs 0.741 (S2-seasonal).
- Label-free k-means: ARI 0.501 (AE) vs 0.327 (S2-seasonal).

## Repository structure

```
notebooks/T05_notebook.ipynb   full pipeline (Google Colab + Earth Engine + scikit-learn)
data/                          block boundaries and labelled sample points
results/tables/                result tables (_ID / _EN) and T05_hasil_ringkas.json
results/figures/               figures (_ID / _EN)
docs/diagrams/                 flowchart, context diagram, level-1 DFD (ID & EN)
```

## License

Code: MIT (`LICENSE`). Data, results and figures: CC BY 4.0.
