# 3-Bit Binary-Weighted Digital-to-Analog Converter

Designed, built, and experimentally characterized a **3-bit digital-to-analog converter (DAC)** using a binary-weighted resistor network and two operational-amplifier stages. The breadboard prototype produced eight distinct, monotonically increasing output levels, with a measured full-scale output of **4.345 V** compared with the theoretical **4.375 V**.

Completed for **ELECENG 2EI4 — Electronic Devices & Circuits I** at McMaster University, Winter 2026.

## Motivation

Digital systems represent information as binary values, while analog circuits operate on continuous voltages and currents. This project explored that interface by implementing a DAC from discrete components and examining how resistor ratios and op-amp behaviour affect conversion accuracy.

The goal was to carry a circuit from theoretical analysis through hardware implementation and measurement, then quantify the differences between its ideal and measured performance.

## Project Highlights

- Derived the DAC transfer function using Kirchhoff’s current law and ideal op-amp analysis.
- Selected resistor values and adapted the implementation to the available component inventory.
- Built and tested the circuit on a breadboard using an **Analog Discovery 3** and **WaveForms**.
- Verified all eight input combinations and evaluated offset error, gain error, and differential nonlinearity.

## Circuit Design

The circuit uses two stages:

1. **Binary-weighted summing amplifier:** Three inputs connect through resistors of R, 2R, and 4R. With a feedback resistance of R/2, the stage assigns each bit its binary weight and produces an inverted analog output.
2. **Unity-gain inverting amplifier:** A second stage reverses the polarity to produce a positive output voltage.

For binary inputs $b_2$, $b_1$, and $b_0$, where $b_2$ is the most significant bit:

$$
V_{\text{out}} = V_{\text{ref}}\left(\frac{b_2}{2}+\frac{b_1}{4}+\frac{b_0}{8}\right)
$$

| Parameter | Design value |
|---|---|
| Resolution | 3 bits / 8 output levels |
| Logic input levels | 0 V and 5 V |
| Reference voltage | 5 V |
| Op-amp supply rails | ±5 V |
| Input resistors | 2.5 kΩ, 5 kΩ, 10 kΩ |
| Summing-stage feedback resistor | 1.25 kΩ |
| Ideal step size | 0.625 V/LSB |
| Ideal full-scale output | 4.375 V |

### Design Trade-offs

I selected the binary-weighted topology because its small component count and direct relationship between resistor values and bit weights made it practical to assemble and troubleshoot for a three-bit implementation.

An R–2R ladder would offer better scalability by requiring only two resistor values. However, the available resistor inventory would have required additional series/parallel combinations, increasing wiring complexity for this prototype.

Component availability also affected the second amplifier stage: two 4.99 kΩ resistors in parallel provided a nominal **2.495 kΩ** input resistance in place of the intended 2.5 kΩ.

## Experimental Validation

Each input was manually connected to either 5 V or ground, and the output was measured for all eight binary codes using the Analog Discovery 3.

| Binary input | Ideal output (V) | Measured output (V) |
|---|---:|---:|
| 000 | 0.000 | 0.036 |
| 001 | 0.625 | 0.653 |
| 010 | 1.250 | 1.236 |
| 011 | 1.875 | 1.873 |
| 100 | 2.500 | 2.484 |
| 101 | 3.125 | 3.121 |
| 110 | 3.750 | 3.733 |
| 111 | 4.375 | 4.345 |

The measured output increased at every code transition, confirming **monotonic operation across all eight codes**.

| Performance metric | Measured result |
|---|---:|
| Zero-code offset | +36 mV |
| Gain error, after subtracting zero-code offset | −1.51% |
| Maximum absolute differential nonlinearity | 0.0672 LSB |
| Largest absolute deviation from ideal output | 36 mV |

The largest step-size deviation occurred at the **001 → 010** transition: the measured step was **0.583 V**, compared with the ideal **0.625 V**. This corresponds to a DNL of **−0.0672 LSB**, or a step 6.72% smaller than ideal.

## Engineering Takeaways

This project demonstrated how resistor matching and nonideal op-amp behaviour can affect DAC accuracy even when the overall transfer characteristic closely follows the theoretical model. Possible contributors to the measured errors include resistor tolerances, amplifier offset, and resistor-ratio mismatch; their individual contributions were not isolated experimentally.

The work strengthened my experience in **analog circuit analysis, component selection, breadboard prototyping, bench measurements, and quantitative error analysis**.

Testing focused on static conversion accuracy. Future improvements could include tighter-tolerance resistors, an R–2R implementation for comparison, and measurements of settling time and switching transients.
