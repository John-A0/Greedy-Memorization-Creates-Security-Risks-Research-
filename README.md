# 🛡️ Greedy Memorization Creates Security Risks  
### Static Malware Detection Using Ensemble Learning on PE Metadata

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![ML](https://img.shields.io/badge/Machine%20Learning-Ensemble-orange)
![Security](https://img.shields.io/badge/Cybersecurity-Malware%20Detection-red)
![Status](https://img.shields.io/badge/Research-Academic-success)

---

## 📌 Abstract

Signature-based detection systems often fail against modern obfuscation techniques. This research evaluates four ensemble learning algorithms for static malware detection using only Portable Executable (PE) header metadata. Although all models achieve over 99.6% accuracy, we demonstrate that they are highly vulnerable to adversarial mimicry attacks, where malware copies benign metadata to bypass detection. This exposes a critical limitation of metadata-based static analysis.

---

## 🎯 Research Objectives

- Compare ensemble learning models on PE metadata  
- Analyze operational trade-offs (False Positives vs False Negatives)  
- Investigate feature importance concentration and greedy learning behavior  
- Test robustness using adversarial PE header manipulation  

---

## 🧪 Models Evaluated

Random Forest (Bagging)  
XGBoost (Boosting)  
LightGBM (Boosting)  
Histogram Gradient Boosting (Boosting)

---

## 📊 Dataset

Total samples: 34,054 Windows PE executables  
Benign: 18,626  
Malware: 15,428  
Features: 54 PE header attributes  
Extraction tool: pefile (Python)  
Split: 80% Training / 20% Testing  

Feature categories include linker versions, OS versions, entry point, image base, section alignment, checksum, and structural header attributes.

---

## ✅ Results Summary

All models achieved very high benchmark performance (>99.6% accuracy):

HistGradientBoosting — Accuracy: 99.80%, FP: 6, FN: 8  
XGBoost — Accuracy: 99.78%, FP: 8, FN: 7  
LightGBM — Accuracy: 99.75%, FP: 7, FN: 10  
Random Forest — Accuracy: 99.65%, FP: 19, FN: 5  

Operational interpretation:  
HistGradientBoosting is best suited for user-facing systems due to lowest false positives, while Random Forest is better suited for backend security due to lowest false negatives.

---

## ⚠️ Feature Importance Risk: Greedy Memorization

Boosting models exhibit extreme dependence on a small number of metadata features, particularly Minor Linker Version. This creates a single point of failure where modifying only one header field can evade detection. Random Forest distributes importance across many features, making it more stable but still not immune to evasion.

---

## 🧨 Adversarial Mimicry Attack

Attack methodology:  
A malware sample initially detected by all models was modified by copying only the linker version metadata from the legitimate Windows calculator (calc.exe). The malicious payload remained unchanged.

Results:  
All models misclassified the modified malware as benign.

HistGradientBoosting — Benign (99.6% confidence)  
LightGBM — Benign (99.3% confidence)  
XGBoost — Benign (97.9% confidence)  
Random Forest — Benign (62% confidence)

Random Forest showed uncertainty but still failed, confirming that metadata-only analysis is fundamentally vulnerable.

---

## ⚠️ Case Study: AnyDesk False Positive

The legitimate remote administration tool AnyDesk.exe was consistently classified as malware due to outdated linker versions and high entropy caused by compression. This shows that models detect structural obfuscation patterns, which may overlap between malware and legitimate privacy tools.

---

## 🧠 Conclusion

Metadata-based ensemble models provide fast and highly accurate malware detection on benchmark datasets, but they lack adversarial robustness. Even simple header manipulation can fully bypass detection. Therefore, PE metadata classifiers should never be used as standalone security solutions.

Recommended deployment:  
Use metadata-based models strictly as a high-speed pre-filtering layer, combined with deeper content inspection methods such as byte-level n-gram analysis, Import Address Table hashing, and dynamic sandboxing.

---

## 📚 Citation

Kostandy, J. (2026).  
Greedy Memorization Creates Security Risks:  
How Metadata Overfitting Enables Trivial Malware Evasion.  
ITMO University.

---

## ⚠️ Disclaimer

This repository is for academic research and educational purposes only. Do not perform malware analysis or evasion testing on systems you do not own or have explicit permission to test.

---

⭐ If you find this research useful, consider starring the repository.
