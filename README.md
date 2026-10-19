# Building-Age-Classification
building age classification from satellite image

#  SEKU Data Science Regional Hackathon (theDSRH)

## Project Overview
For the SEKU Data Science Regional Hackathon, our team tackled a complex unsupervised domain adaptation challenge: **Can a machine learning model trained on building age data from one city (Madrid) successfully transfer its knowledge and predict building ages in another city (Amsterdam) using 42 years of Landsat satellite data?**

Instead of treating this as a standard classification problem, we investigated how spatial features and representations transfer across different urban environments with distinct historical and material characteristics.

---

## Key Methodology & Highlights

* **Data Cleaning & Preprocessing:** Processed 42 years of annual Landsat satellite data across 76,263 locations in Madrid and 25,992 locations in Amsterdam. Handled scene contamination, removed bad readings, and applied linear interpolation for interior gaps while preserving genuine age-related signals.
* **Feature Engineering:** Extracted and analyzed **81 features** grouped into absolute levels, time-series shape, changes over time, spectral indices, and metadata. Identified which features carried age-related signals versus city-specific traits (e.g., noting that features like `SWIR2_jump_size` transfer well, while raw spectral bounds reflect local environments).
* **Robust Spatial Validation:** Implemented **spatially blocked cross-validation** to prevent data leakage caused by spatial autocorrelation between neighboring Landsat pixels.
* **Domain Adaptation Strategy:** Developed a custom transfer method involving domain standardisation and prototype blending:
  > *"Carry the class locations, but re-learn the geometry locally."*
  * Achieved a macro F1 score of **0.5605 with only 25 local labels per class**, proving that a small amount of target-domain data dramatically improves transfer performance.

---

## Results Summary

| Model / Approach | Evaluation Context | Macro F1 Score |
| :--- | :--- | :--- |
| **Madrid Baseline Model** | Spatially blocked CV | **0.5954** |
| **Amsterdam (Zero-Shot)** | No local labels | **0.4553** |
| **Amsterdam (25 Labels/Class)** | Prototype Blending | **0.5605** |
| **Amsterdam (200 Labels/Class)**| Prototype Blending | **0.5766** |

---

## Tech Stack
* **Language:** Python
* **Libraries:** Pandas, NumPy, Scikit-learn, SciPy, Seaborn, Matplotlib
* **Modelling:** Class-Balanced Random Forest (300 trees), 1D-CNN exploration, Domain Adaptation & Prototype Blending Framework

---

## Future Improvements
* Incorporating broader spatial context using neighboring pixel structures.
* Implementing an ordinal loss function to penalize misclassifications across distant age classes less severely than adjacent classes.
* Testing the pipeline on a third city to validate broader generalizability.
