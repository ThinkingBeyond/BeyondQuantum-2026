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

## Important parameters in a protocol
BB84 is characterized by 2 very important parameters: the Quantum Bit Error Rate and the key rate. These 2 parameters indicate if the protocol will be finished and considered secure, and also the efficiency of the protocol round.
We start with the QBER: After the sifting process Alice and Bob choose from their sifted a range of subsets equivalent in the indices, and publicly compare their bits. QBER is the percentage of differing bits from the total number of the bits compared. Of course, because the bits were publicly discussed, they are discarded from the sifted keys.
QBER indicates the feasibility of the protocol round. If a protocol round has a QBER higher than 11%, then it is considered unsafe, because Eve has eavesdropped a high number of bits, indicated by the QBER.
The second important parameter is the key-rate. It can be viewed from 2 perspectives: as a rate of the efficiency over time or over the number of total pulses (we can imagine pulses of single photons for each bit). It follows how many or how fast the secure bits remain in the processed final key.

### Modeling the Attacks

In this research Side-Channel attacks were modeled using their corresponding QBER values. ***These QBER values were selected based on the literature.***

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

## Discussing the Results of the Analysis

### The BB84 Key Generation under different Side-Channel Attacks

<img width="790" height="587" alt="image" src="https://github.com/user-attachments/assets/262f7552-7393-4d19-8743-12f067e0feb5" />

This graph shows how the key generation is affected under multiple attacks. Concluded from the graph that the Key rate decreases as the QBER increases.

For the Intercept-Resend atttack (QBER=0.20) we can notice that the key rate went below zero which means that the key bits are totally damaged. Therefore Alice and Bob need to re-establish the BB84 connection.

### The failure of QBER to detect some Side-Channel attacks

<img width="790" height="590" alt="image" src="https://github.com/user-attachments/assets/cc3d8828-75af-42a0-8af1-24e981ee183f" />

The blue straight line introduces a naive assumption that low QBER implies low information leakage.

The red dot represents the detector blinding attack which invalidates that naive assumption.

The graph shows that the detector blinding attack violates that assumption. The Detector Blinding attack do not increase the QBER above the standered threshold which will cause neither Alice or Bob to notice that their connection is compormised.

What we finally conclude from that graph is the QBER fails to detect some side-channel attacks. Therefore **Hradware-Level monitoring mechanisms** are requird for those attacks.

## Limitations of BB84 and solutions
The QBER measures how much Eve has interacted in the data transmission phase and how much knowledge she has gathered by measuring and disturbing the photons. 11% is an industry-standard QBER value at which it is considered that Eve has too much knowledge about the symmetric keys, and the protocol has to be discarded. There is a solutions of 2 additional steps which can be implemented and enhance the security of the key up to this point in the protocol.

## Advanced distillation
A simple and reliable method to diminish the QBER is reducing the number of differing equivalent bits in the 2 sifted keys. Alice decides on a subset of random bits in her key, and tells Bob a hint about her subset, without telling explicitly the bits. The hints can be simple like the parity of the number of 1 bits, or more advanced Low-Density Parity-Checks and Polar Codes. If 2 equivalent subsets do not match from the hints, they are discarded. This is an efficient way to eliminate the bits causing QBER, but the method also deletes good secure bits with them.

## Noise preprocessing.
Advanced distillation is the first step, and after it follows noise preprocessing. At this point we assume that Eve has knowledge about bits in the sifted key (values of bits, positions, information about subsets, etc.). Alice can induce fake noise in the key by changing a certain number of bit's values in her sifted key. This noise has to be later corrected in an error correction step, but the gain is that Eve's knowledge about the changed bits and the neighboring subsets is wrong, and when she will to attack the result will be incorrect.
Regarding how many bits have to be changed in order to cause enough disturbance for Eve is given by the formula

## Conclusions 

* Although QBER is succesful in detecting the intercept-Resend attack, but it fails for some other Side-Channel attacks.
* The Time-shift and the Detector Blinding attacks do not increase the QBER above the standered 11% threshold, which makes them undetectable using the QBER.


## Future Work

Detecting the Time-shift and the Detector Blinding attacks require hardware level monitoring mechanisms. Photocurrent mechanism for the Detector Blinding attack, Time Histogram Analysis for the Time-shift attack. 

## References

[1] [Quantum Cryptography: Public Key Distribution and Coin Tossing (Bennett & Brassard, 1984)](https://ieeexplore.ieee.org/document/1055638)

[2] [Hacking Commercial Quantum Cryptography Systems by Tailored Bright Illumination (Lydersen et al., 2010)](https://arxiv.org/abs/1008.4593)

[3] [Time-Shift Attack in Practical Quantum Cryptosystems (Qi et al., 2007)](https://arxiv.org/abs/quant-ph/0512083)

> The research poster for this project can be found in the [BeyondQuantum Proceedings 2026](https://thinkingbeyond.education/beyondquantum_proceedings_2026/).

