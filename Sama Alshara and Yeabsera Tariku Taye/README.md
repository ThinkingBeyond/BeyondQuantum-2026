![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# How Quantum Feature Maps affect QSVM Performance
***Provide a description of your project including*** 

1. motivating your research question
2. stating your research question
3. explaining your method and implementation
4. Briefly mention and discuss your results
5. Draw your conclusions
6. State what future investigations 
7. State your references 

### Further Guidance: Formating
- Structure this readme using subsections
- Your job is to 
    - keep it clear
    - provide sufficient detail, so what you did is understandable to the reader. This way other researchers and future cohorts of BeyondQuantum will be able to build on your research
    - List all your references at the end
- utilise markdown like *italics*, **bold**, numbered and unnumbered lists to make your document easier to read
- if you refer to links use the respective markdown for links, e.g. `[ThinkingBeyond](https://thinkingbeyond.education/)`
- If you have graphs and pictures you want to embed in your file use `![name](your_graphic.png)`
- If you want to present your results in a table use
    | Header 1            | Header 2  |
    |---------------------|-----------|
    | Lorem Ipsum         | 12345     |

**Tip:** Use tools to create markdown tables. For example, Obsidian has a table plugin, that makes creating tables much easier than doing it by hand.

## Research Question

Our research question is "How does the choice of Quantum Feature Map affect QSVM performance? How does it compare to a classical SVM?"
To further clarify, we will be testing out 4 different feature maps (two built in and two modified) and comparing the performance of the QSVMs to each other. Furthermore, by comparing these QSVMs to a Classical SVM, it will show whether Quantum Machine Learning can be a competitor or if this research is a theoretical exploration.

## Motivation

Explain your motivation for your chosen research question here.

## Abstract

Quantum Machine Learning (QML) is an emerging interdisciplinary field that explores the use of quantum computing to potentially enhance classical machine learning techniques. A key challenge in QML is encoding classical data into quantum states, known as quantum data encoding, which is achieved using quantum feature maps. In this work, we implement and systematically compare the Z Feature Map, ZZ Feature Map, and enhanced versions of these feature maps with increased circuit depth and entanglement. These are integrated into a Quantum Support Vector Classifier (QSVC) using a quantum kernel evaluated in simulation. We train and evaluate these models on the Wisconsin Diagnostic Breast Cancer (WDBC) dataset to analyze how feature map design impacts classification performance. Our results show that, for this dataset and experimental setup, the Enhanced Z Feature Map achieves the best performance, reaching an F1-score of 0.9718, highlighting the relevance of feature map design in this context.

## Overview of Key Concepts 
- *Support Vector Machines (SVM)*: are a widely used classical machine learning algorithm that classifies data by finding an optimal hyperplane in a high-dimensional feature space. They work by finding the optimal hyperplane that separates data points of different classes with the maximum margin
- *Principal Component Analysis (PCA)*: PCA is a dimensionality reduction technique widely used in data analysis and machine learning. It transforms a high-dimensional dataset into a smaller set of uncorrelated variables called principal components, while retaining most of the original information.
- *QSVMs*: QSVM extends this approach by using quantum feature maps to encode classical data into a quantum Hilbert space, enabling the evaluation of quantum kernels.
- *Feature Maps*: A technique, implemented via parameterized circuits, that encodes classical data into quantum states, enabling quantum algorithms to operate in high-dimensional Hilbert spaces which potentially revealing patterns a Classical model may miss.

## Methodology 
**Dataset**
**Prepraration**
**Classical SVM**
**Quantum Scaling**
**ZZ & Z Feature Map (Built-in)**
**Modified Feature Maps**
**Metrics**
## Results
## Conclusion
## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

(Temporary listing of references)

  Akpinar, Emine, et al. “Evaluating the Impact of Different Quantum Kernels on the Classification Performance of Support Vector Machine Algorithm: A Medical Dataset Application.” arXiv:2407.09930, arXiv, 19 July 2024. arXiv.org, https://doi.org/10.48550/arXiv.2407.09930.
  
  "1.4. Support Vector Machines.” Scikit-Learn, https://scikit-learn/stable/modules/svm.html.
  
  Montalbán, Iraitz. “Quantum Computing Handbook.” Quantum Computing Handbook, 25 June 2025, https://iraitzm.github.io/qc-handbook/.

  QSVC - Qiskit Machine Learning 0.9.0. https://qiskit-community.github.io/qiskit-machine-learning/stubs/qiskit_machine_learning.algorithms.QSVC.html#qiskit_machine_learning.algorithms.QSVC. 


 

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)

**Tip**: *If you have you references in BibTex, Google Scholar or Zotero*
1. Create/copy a list into ChatGPT
2. Ask it to turn it into an unsorted list in markdown

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

