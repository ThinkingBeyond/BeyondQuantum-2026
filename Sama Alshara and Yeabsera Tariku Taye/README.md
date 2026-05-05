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
Everyone has heard of classical machine learning and has likely seen its strong performance across a wide range of domains. Now, researchers, doctors, and machine learning practitioners are actively exploring what role it can reliably play in medicine.
But what about quantum machine learning?
In theory, quantum models should be able to capture patterns that classical models cannot. So naturally, the question is: does it actually have a place in this race?
Quantum machine learning explores what happens when quantum systems, by leveraging properties such as superposition, are used to learn from data. However, this introduces a fundamental challenge: how classical data, such as medical measurements, can be encoded into quantum systems?
We want to better understand this challenge  Specifically, we investigate how different quantum feature maps influence the performance of Quantum Support Vector Machines (QSVMs), and whether these models can meaningfully compete with well-established classical approaches in a high-stakes context.


## Abstract

Quantum Machine Learning (QML) is an emerging interdisciplinary field that explores the use of quantum computing to potentially enhance classical machine learning techniques. A key challenge in QML is encoding classical data into quantum states, known as quantum data encoding, which is achieved using quantum feature maps. In this work, we implement and systematically compare the Z Feature Map, ZZ Feature Map, and enhanced versions of these feature maps with increased circuit depth and entanglement. These are integrated into a Quantum Support Vector Classifier (QSVC) using a quantum kernel evaluated in simulation. We train and evaluate these models on the Wisconsin Diagnostic Breast Cancer (WDBC) dataset to analyze how feature map design impacts classification performance. Our results show that, for this dataset and experimental setup, the Enhanced Z Feature Map achieves the best performance, reaching an F1-score of 0.9718, highlighting the relevance of feature map design in this context.

## Overview of Key Concepts 
- *Support Vector Machines (SVM)*: are a widely used classical machine learning algorithm that classifies data by finding an optimal hyperplane in a high-dimensional feature space. They work by finding the optimal hyperplane that separates data points of different classes with the maximum margin
- *Principal Component Analysis (PCA)*: PCA is a dimensionality reduction technique widely used in data analysis and machine learning. It transforms a high-dimensional dataset into a smaller set of uncorrelated variables called principal components, while retaining most of the original information.
- *QSVMs*: QSVM extends this approach by using quantum feature maps to encode classical data into a quantum Hilbert space, enabling the evaluation of quantum kernels.
- *Feature Maps*: A technique, implemented via parameterized circuits, that encodes classical data into quantum states, enabling quantum algorithms to operate in high-dimensional Hilbert spaces which potentially revealing patterns a Classical model may miss.

## Methodology 
- **Dataset**
For this study, we decided to evaluate our models in a high-stakes situation, cancer diagnosis. We use the University of Wisconsin Breast Cancer Dataset, a widely recognized benchmark in machine learning. The dataset consists of 30 features extracted from digitized images of fine needle aspirates (FNA) of breast masses. These features describe characteristics of cell nuclei, including radius, texture, smoothness, and compactness. This is a binary classification task, where:
-0 represents benign (non-cancerous) tumors
-1 represents malignant (cancerous) tumors
=The dataset contains 569 samples, with a relatively balanced class distribution: 212 Malignant - 357 Benign

- **Prepraration**
The first task to complete was actually preparing our dataset to be used.  
1) split into training and testing sets using an 80/20 ratio to ensure reliable model evaluation.
2) The features were then standardized using StandardScaler, which centers the data and scales it to unit variance so that all features contribute equally to the model.
3)  Following this, Principal Component Analysis (PCA) was applied to reduce the dimensionality from 30 features to 4 principal components. This step preserves the majority of the dataset’s variance (44%, 19%, 9%, 7%) while simplifying the feature space, making it more suitable for later use in the QSVM
- **Classical SVM**
To establish a reference point to compare the QSVM performance with, we first implemented a classical Support Vector Machine (SVM) using an RBF (Radial Basis Function) kernel. This model serves as a baseline to see whether Quantum Support Vector Machines (QSVMs) provide any meaningful performance advantage.
The SVM was trained on the PCA-reduced feature set, with the regularization parameter set to C=10. Training time was recorded to allow for runtime comparisons with quantum models. After training, predictions were generated on the test set to assess performance.
Using a classical model as a baseline is essential in this context. While quantum machine learning introduces more complex data representations, it is important to determine whether these added complexities directly correlates into measurable improvemnents in performance over well-established classical methods. Without this comparison, it would be difficult to assess the practical value of QSVMs.
- **Quantum Scaling**
-Before applying quantum feature maps, we had to ensure the data was ready to be put in a quantum system. The data was scaled using a MinMaxScaler to the range [0,0.5]. This step is vital when working with quantum circuits, as classical features are encoded into qubits through parameterized rotation gates.
=Since hese rotations are periodic (e.g., rotations differing by multiples of 2π can produce identical quantum states), large or unbounded feature values can lead to different data points being mapped to indistinguishable quantum states. For example, rotations of π and 3π may encode the same information, reducing the model’s ability to differentiate between inputs.
-By constraining the feature range, we ensure that encoded data points remain distinguishable in the quantum state space, preserving meaningful variation for the model to learn from.
=This step proved to be a make or break step in building QSVMs (or any Quantum-Classical hybrid algorithm). Without quantum scaling, model performance dropped significantly, reaching an accuracy of approximately 0.56, essentially no better than a coin flip. This highlights the sensitivity of quantum models to proper data encoding and reinforces the importance of careful preprocessing in quantum machine learning.
- **ZZ & Z Feature Map (Built-in)**
    -After preparing the data and applying quantum scaling, we constructed Quantum Support Vector Machines (QSVMs) using built-in feature -maps from Qiskit. These feature maps define how classical data is encoded into quantum states and play a central role in model performance.
    -We focused on two feature maps: Z feature maps and ZZ feature maps. 
    -The Z feature map uses single-qubit rotation gates (specifically RZ gates) to encode each feature independently. Each input feature controls the rotation of a single qubit, meaning the resulting representation captures only individual feature contributions, with no interactions between them.
    -In contrast, the ZZ feature map extends this encoding by introducing pairwise interactions between qubits through entangling ZZ-rotations. These operations encode products of features (x<sub>i</sub>x<sub>j</sub>), allowing the model to capture relationships between pairs of features.
- **Modified Feature Maps**
- *ZZ (Modified)* The custom ZZ feature map uses a circular (ring) entanglement structure, where each qubit interacts only with its nearest neighbors in a closed loop (e.g., qubit 0 ↔ 1 ↔ 2 ↔ 3 ↔ 0). This design ensures uniform connectivity across all qubits. The encoding process consists of:
1) Superposition initialization using Hadamard gates
2) Single-qubit encoding via RZ rotations
3) Pairwise interaction encoding using a CNOT–RZ–CNOT structure
4)The interaction term: (π−x<sub>i</sub>)(π−x<sub>j</sub> was introduced to encode nonlinear relationships between neighboring features. Centering the encoding around π helps maintain distinguishability in the quantum state space, while the multiplicative form explicitly captures feature dependencies.
    -Overall, this design balances expressivity (through nonlinear feature interactions) with structured entanglement (through circular connectivity).
- *Z (Modified)* The custom Z feature map follows the same single-qubit RZ encoding scheme as the standard version but introduces full entanglement across all qubits. Unlike the standard Z feature map, which treats features independently, this variant allows information to be connected globally through the circuit via entanglement. This increases the expressiveness of the representation without explicitly introducing pairwise product terms like the ZZ feature map.
-**Metrics**
-To compare the performance of both classical and quantum models, we used standard ML metrics that capture different aspects of classification quality, as well as runtime to see computational efficiency. All classification metrics are based on the confusion matrix, which summarizes model predictions into four categories:
1) True Positive (TP): The model correctly predicts a malignant tumor as malignant
2) True Negative (TN): The model correctly predicts a benign tumor as benign
3) False Positive (FP): The model incorrectly predicts a benign tumor as malignant
4) False Negative (FN): The model incorrectly predicts a malignant tumor as benign
-------------------------------------------------------------------------------------
1) Accuracy (measures % of correct predictions) : (TP + TN) / (TP + TN + FP + FN)
2) Precision (Measures how many predicted malignant cases are actually correct.) = TP / (TP + FP)
3) Recall (Measures how many actual malignant cases are correctly identified.) = TP / (TP + FN)
This is particularly important in medical applications, where missing a malignant case can have serious consequences. 
4) F1 Score (Provides a balance between precision and recall.) = 2 * (Precision * Recall) / (Precision + Recall)
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

  https://www.kaggle.com/datasets/yasserh/breast-cancer-dataset


 

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)

**Tip**: *If you have you references in BibTex, Google Scholar or Zotero*
1. Create/copy a list into ChatGPT
2. Ask it to turn it into an unsorted list in markdown

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

