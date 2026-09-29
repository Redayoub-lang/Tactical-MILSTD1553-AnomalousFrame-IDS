# MIL-STD-1553B Avionics Bus Intrusion Detection Engine

![C++17](https://img.shields.io/badge/Language-C%2B%2B17-blue)
![Avionics Security](https://img.shields.io/badge/Domain-Embedded%20Cybersecurity-red)
![Developer](https://img.shields.io/badge/Developer-Ayoub%20Lahmar-brightgreen)

A deterministic, ultra-low latency hardware frame inspector for military avionics databuses (**MIL-STD-1553B / STANAG 3838**). Detects command word spoofing, parity corruption, and Bus Controller hijacking in real time.

Implemented by **Ayoub Lahmar** ([@Redayoub-lang](https://github.com/Redayoub-lang)).

## 📐 Bus Protocol Invariant

Word validation requires hardware synchronization verification \(S_{\text{sync}}\) and odd parity bit checking over the 20-bit transmission frame:

$$
P_{\text{odd}} = \left( \sum_{i=1}^{16} b_i \right) + b_{\text{parity}} \equiv 1 \pmod 2
$$

Command word Remote Terminal Address (RTA) filtering blocks unauthorized command injection:

$$
\text{Status} = \begin{cases} \text{VALID}, & \text{if } \text{RTA} = \text{RTA}_{\text{expected}} \land P_{\text{odd}} = 1 \\ \text{ALERT}, & \text{otherwise} \end{cases}
$$

## 💻 Build & Compile

```bash
g++ -std=c++17 -O3 main.cpp -o AvionicsIDS
./AvionicsIDS
