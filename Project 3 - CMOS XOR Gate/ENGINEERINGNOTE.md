# Transistor-Level CMOS XOR Gate

Designed, built, and tested a **CMOS XOR gate** using complementary PMOS and NMOS transistor networks. Verified all four input combinations, measured output logic levels, and characterized switching behaviour using an **Analog Discovery 3** and **WaveForms**.

Completed for **ELECENG 2EI4 — Electronic Devices & Circuits I** at McMaster University, Winter 2026.

## Motivation

Logic gates are the building blocks of digital systems, but their behaviour depends on the analog characteristics of the transistors implementing them. This project explored that connection by translating an XOR Boolean expression into a physical CMOS circuit.

The goal was to move beyond truth-table verification and investigate how transistor sizing, pull-up and pull-down paths, and practical hardware constraints influence output voltage levels and propagation delay.

## Project Highlights

- Derived a CMOS-compatible XOR implementation using Boolean algebra and De Morgan’s theorem.
- Implemented complementary PMOS pull-up and NMOS pull-down networks on a breadboard.
- Analyzed transistor sizing requirements to balance pull-up and pull-down drive strength.
- Verified all four input combinations using digital test patterns.
- Measured output HIGH/LOW levels, rise and fall times, and propagation delays.

## Logic and Circuit Design

The XOR function produces a HIGH output when its inputs differ:

$$
Y = A \oplus B = \overline{A}B + A\overline{B}
$$

| Input A | Input B | Output Y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

Rewriting the expression gives:

$$
Y = \overline{AB + \overline{A}\,\overline{B}}
$$

This form maps to a complementary CMOS implementation:

- **Pull-down network:** Conducts when both inputs are equal, pulling the output toward ground.
- **Pull-up network:** Conducts when the inputs differ, pulling the output toward the supply voltage.
- **CMOS inverters:** Generate the complemented inputs required by the networks.

## Transistor Sizing and Implementation Constraints

The sizing analysis used an approximate electron-to-hole mobility ratio of **2.5:1**. Under this assumption, a larger PMOS width-to-length ratio is needed to provide drive strength comparable to an NMOS device.

The proposed ratios were:

$$
\left(\frac{W}{L}\right)_n = 2,
\qquad
\left(\frac{W}{L}\right)_p = 5
$$

Both networks contain conducting paths with two transistors in series. These series devices increase effective path resistance and must be considered when evaluating switching speed.

The physical prototype used transistors supplied in the course component kit, whose dimensions were fixed by the manufacturer. Therefore, the proposed sizing could be analyzed theoretically but could not be directly implemented or optimized on the breadboard.

## Hardware and Test Setup

| Tool or component | Purpose |
|---|---|
| PMOS and NMOS transistors | CMOS logic networks and input inverters |
| Breadboard | Circuit assembly |
| Analog Discovery 3 | Input generation and output measurement |
| WaveForms | Pattern generation, logic analysis, and oscilloscope measurements |
| 5 V supply | Circuit power |

### Functional Verification

The AD3 digital channels were configured as follows:

| Channel | Connection | Configuration |
|---|---|---|
| DIO 0 | Input A | 2 kHz clock |
| DIO 1 | Input B | 1 kHz clock |
| DIO 2 | Output Y | Logic analyzer input |

The input patterns exercised all four binary combinations. The captured output matched the XOR truth table.

### Output Logic Levels

Output levels were measured with one input held HIGH while the other input switched.

| Test configuration | Output HIGH | Output LOW |
|---|---:|---:|
| A switching, B held HIGH | 5.000 V | 6.61 mV |
| B switching, A held HIGH | 5.000 V | 18.85 mV |

Both configurations produced output levels close to the 5 V supply and ground.

## Timing Characterization

Oscilloscope measurements were used to evaluate output transitions and estimate propagation delays between input and output midpoint crossings.

| Metric | Reported measurement |
|---|---:|
| Output rise time | 316.66 µs |
| Output fall time | 298.50 µs |
| Low-to-high propagation delay | 160.24 µs |
| High-to-low propagation delay | 164.31 µs |
| Average propagation delay | 162.28 µs |

The average propagation delay was calculated as:

$$
t_p = \frac{t_{pLH} + t_{pHL}}{2}
= \frac{160.24 + 164.31}{2}
\approx 162.28\ \mu\text{s}
$$

These measurements characterize the assembled breadboard circuit under the tested conditions. They include the effects of the devices, circuit loading, wiring, and measurement setup; those contributions were not isolated individually.

## Engineering Takeaways

This project connected **Boolean logic, transistor-level circuit design, and hardware verification**. Functional testing established correct XOR operation, while voltage and timing measurements showed the physical behaviour behind the digital truth table.

The work strengthened my experience in:

- Translating Boolean expressions into complementary CMOS networks.
- Relating transistor sizing and series conduction paths to drive strength.
- Building and testing transistor-level circuits.
- Using logic analyzer and oscilloscope measurements to evaluate hardware.

Future work could compare measured results with transistor-level simulation, investigate the sources of the observed transition times, and evaluate switching behaviour under controlled output loads.
