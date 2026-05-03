![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# How does the implementation of *n* logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of simplified molecular library search?

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

**The central inquiry of this study is:** *"How does the implementation of n logical constraints affect the search space and runtime of Grover’s Algorithm, investigated in the context of a simplified molecular library search?"*

**Core Objectives:**
Grover’s Algorithm provides a theoretical quadratic speedup for unstructured search problems where classical alternatives are limited. Our research explores the practical boundary of this speedup by *focusing on primary factors:*
- **Constraint Complexity (*n*):** We investigate how increasing the number of logical filters — such as toxicity, nitrogen presence, molecular size, and the presence of a ring — impacts the construction of the quantum Oracle.
- **Success Probability vs. Efficiency:** While additional constraints narrow the search space, they simultaneously increase circuit depth. We aim to identify the threshold where these constraints transition from being helpful filters to becoming a source of "noise" or complication that degrades the probability of a successful search.
- **Technical Context:** To address this question, we utilized a 4-qubit circuit in Qiskit to navigate a dataset of 16 molecules. Each molecule is mapped to a unique 4-bit code based on specific biochemical properties. This setup allows us to precisely monitor the phenomenon of over-rotation — a state where applying too many Grover iterations (*k*) causes the quantum state vector to rotate past the target solution, effectively "losing" the signal of the correct molecule.
- **Theoretical Significance:** By finding the precise balance of iterations (*k*) required for varying logical constraints, this research demonstrates how quantum searching can be optimized for identifying viable drug candidates in simplified chemical scenarios. Our findings highlight that maintaining accuracy in a quantum search is not just about having more constraints, but about managing the quantum state to avoid signal degradation.

## Motivation

In pharmaceutical research, virtual screening is an "unstructured search" problem—checking millions of potential drug candidates one by one. We chose this research question to test the efficiency of Grover's Algorithm, which theoretically offers a quadratic speedup over classical methods. By mapping molecular properties to logical constraints, we aim to identify the optimal threshold where quantum searching maintains high success probability before circuit complexity or over-rotation degrades the results.

## Your next subsection

Continue working through the points listed above with the help of sensibly named subsections. 

If you want to see some good examples of README files check out:
- [Example 1](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/warenya-loulia/README.md)
- [Example 2](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/shaana-karuna/README.md)

[ ... ]

## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

List all your references here. Remember to put links into markdown. For example:

1.  Einstein, A. (1905). *On the Electrodynamics of Moving Bodies*. Annalen der Physik, 17, 891-921. [Internet Archive](https://archive.org/details/einstein-1905-relativity)

**Tip**: *If you have you references in BibTex, Google Scholar or Zotero*
1. Create/copy a list into ChatGPT
2. Ask it to turn it into an unsorted list in markdown

---

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

