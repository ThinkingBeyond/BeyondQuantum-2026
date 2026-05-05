![BeyondQuantum Banner for Research Projects](../BeyondQuantum_Banner_Research_Projects_2026.png)

# Analysis of Side-Channel Attacks on the BB84 protocol and Discovering the Mathematical and Statistical Limitations of BB84

***Provide a description of your project including*** 

1. motivating your research questio
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

## Research Questions

Our research project tackeled two research questions.

**1- How do different Side-Channel Attacks affect the security and the key generation of the BB84 protocol? and how to detect them using QBER?**

We analyzed how different side-Channel attacks like the **Intecept-Resend, Time-Shift, and the Detector Blinding attacks** manipulate the hardware of the Quantum Key Distribution device to allow an Eavesdropper (Eve) gain information about the secret key. Also Studied whether the Quantum Bit Error rate (QBER) is sufficient to detect the Time-shift and the Detector Blinding attacks.

**2-Which are the mathematical and statistical limitations of the BB84 protocol?**

## Motivation

Our motivation for the projects is the potential BB84 has for mass-applications in industries like telecommunications and internet traffick. Looking at the basic implementaton, it is not that complicated to implement with physics instruments and a well calculated environment.

The BB84 Protocol security depends on the hardware of the QKD device, which can have many imperfections. These imperfections are potential vulnerabilities which allow Eve to apply Side-Channel attacks. Many systems depend on the QBER to detect attacks, but for some side-channel attacks like the time-shift and the detector blinding the QBER does not change significantly, which makes the QBER insufficient for those attacks.

## Methods and Implementations

### Modeling the Attacks

In this research Side-Channel attacks were modeled using their corresponding QBER values. ***These QBER values were selected from the literature.***

The highest QBER is assigned to the Intercept-Resend attack as it causes the highest disturbance, therefore,  its theoretical QBER value is nearly 15%-25% [1], follows the Time-Shift attack with theoretical QBER value between 1% − 4%  as it cause moderate disturbance[3] , and finally the  Detector Blinding attack with theoretical QBER value of nearly 0% [2]

 | Attack Scenario        | Modeled QBER (e) |
|----------------------|------------------|
| No Attack (Baseline) | 0.01 (1%)        |
| Intercept-Resend     | 0.15 (15%)       |
| Time-Shift           | 0.05 (5%)        |
| Detector Blinding    | 0.001 (0.1%)     |

### The Key Rate as a Function of QBER

The key rate is how many bits were transmitted from the sender to the receiver. Can be represented as 

$$
R = 1 - 2H(\text{Q})
$$

Q is the Quantum Bit Error Rate (QBER) value 

H is the Binary Entropy Function

R is the Key Rate 

### The Binary Entropy Function

Function that is used to calculate Eve's information (Leakage), also used in the Key Rate function.

$H(\text{QBER}) = -\text{QBER} \log_2(\text{QBER}) - (1 - \text{QBER}) \log_2(1 - \text{QBER})$

If you want to see some good examples of README files check out:
- [Example 1](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/warenya-loulia/README.md)
- [Example 2](https://github.com/ThinkingBeyond/BeyondAI-2024/blob/main/shaana-karuna/README.md)

[ ... ]

## Future Work

State and explain what follow-up research could be conducted based on your work.

## References

[1] [Quantum Cryptography: Public Key Distribution and Coin Tossing (Bennett & Brassard, 1984)](https://ieeexplore.ieee.org/document/1055638)

[2] [Hacking Commercial Quantum Cryptography Systems by Tailored Bright Illumination (Lydersen et al., 2010)](https://arxiv.org/abs/1008.4593)

[3] [Time-Shift Attack in Practical Quantum Cryptosystems (Qi et al., 2007)](https://arxiv.org/abs/quant-ph/0512083)

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

