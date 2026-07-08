# Design Decisions

This document outlines the engineering decisions made during the design of the **Universal 24W Isolated AC-DC Flyback Power Supply**.

---

# Why I Selected the MYRRA 74030 Transformer

The transformer is the most critical component in an isolated flyback converter, influencing efficiency, regulation, thermal performance, and safety.

Instead of using an undocumented generic transformer, I selected the **MYRRA 74030** because it is a commercially manufactured transformer with published winding information, reinforced insulation, and documented compatibility with several offline flyback controllers.

The transformer provides:

- 4 kV reinforced isolation
- 6 mm creepage distance
- Universal 85–265 VAC operation
- 30 W power capability
- Published winding specifications

Using a transformer with manufacturer documentation significantly reduces design risk while improving reliability and repeatability.

---

# Why I Chose the TOP244Y Controller

Rather than using a low-cost controller with limited documentation, I selected the **Power Integrations TOP244Y** because it is supported by extensive reference designs, application notes, and proven commercial implementations.

The MYRRA 74030 transformer is specifically listed as compatible with the TOP244Y for universal input operation, allowing the design to build upon a validated ecosystem rather than reverse-engineering an undocumented solution.

Advantages include:

- Extensive application documentation
- Proven commercial reliability
- Built-in protection features
- Excellent EMI performance
- Large engineering community and reference material

---

# Why the Flyback Output is 12V / 2A

Although the original design target was:

- 12V @ 1A
- 5V @ 1A

both outputs may be required simultaneously.

Since the 5V rail is generated from the 12V rail using a buck converter, the flyback stage must supply:

- External 12V load
- Power consumed by the buck converter
- Conversion losses

Therefore, the flyback converter is designed for:

**12V @ 2A (24W)**

This provides sufficient headroom for:

- Continuous full-load operation
- Buck converter input power
- Startup transients
- Component derating
- Thermal margin

Operating the 30W transformer below its maximum rating also improves efficiency and long-term reliability.

---

# Why Generate 5V Using a Buck Converter

Instead of designing a dual-output flyback converter with separate regulated secondary windings, the design regulates a single **12V output** and derives **5V** using a high-efficiency buck converter.

Advantages include:

- Better voltage regulation
- Improved cross-load performance
- Simpler transformer design
- Easier compensation
- Lower output ripple
- Reduced design complexity
- Easier debugging and testing

Modern synchronous buck converters typically exceed **90% efficiency**, making this approach highly efficient while maintaining excellent output regulation.

---

# Why Reinforced Creepage and Isolation Were Used

Since this power supply connects directly to the AC mains, electrical isolation between the primary and secondary circuits is essential.

The PCB incorporates:

- Reinforced isolation barrier
- Minimum 6 mm creepage distance
- Isolation slot beneath the transformer
- Isolation slot beneath the optocoupler
- Separate primary and secondary copper pours
- No routing across the isolation barrier

These measures improve electrical safety while reducing the risk of dielectric breakdown during long-term operation.

---

# Why Input Protection Components Were Included

An offline AC-DC converter is exposed to:

- Mains voltage surges
- Inrush current
- Differential-mode noise
- Common-mode noise

The input stage therefore includes:

| Component | Purpose |
|-----------|---------|
| Fuse | Protects against catastrophic faults |
| MOV | Absorbs mains surge voltages |
| NTC Thermistor | Limits inrush current |
| Common-Mode Choke | Reduces conducted EMI |
| X-Class Capacitor | Suppresses differential-mode noise |
| Y-Class Capacitor | Suppresses common-mode noise while maintaining isolation |

These components improve:

- Safety
- Reliability
- EMC performance
- Regulatory compliance

---

# Why I Used a Commercially Available Transformer

Designing a flyback transformer requires:

- Core selection
- Air-gap calculation
- Turns ratio calculation
- Wire gauge selection
- Leakage inductance optimization
- Thermal validation
- Safety insulation design

Rather than designing a custom transformer, this project uses a commercially manufactured transformer with documented characteristics and safety approvals.

This reflects common industrial practice, where qualified magnetic components are often preferred over custom designs unless high-volume production justifies dedicated transformer development.

---

# Why the Flyback Topology Was Chosen

For power levels below approximately **50W**, the flyback converter offers the best balance of simplicity, cost, efficiency, and isolation.

Advantages include:

- Single magnetic component
- Galvanic isolation
- Universal input capability
- Low component count
- Compact PCB footprint
- Mature design ecosystem
- Excellent efficiency in the 20–30W range

For a universal-input **24W** power supply, the flyback topology provides an ideal balance between performance, manufacturability, and design complexity.

---

# Project Design Philosophy

The objective of this project is not simply to produce a functioning power supply, but to develop a **professionally engineered offline SMPS** using industry-standard design practices.

Key design goals include:

- Reliability over minimum cost
- Component selection based on manufacturer documentation
- Compliance with high-voltage PCB layout practices
- Robust thermal performance
- Proper EMI mitigation
- Comprehensive documentation
- Reproducible design decisions

The final result aims to demonstrate not only PCB design skills but also a solid understanding of power electronics, isolation techniques, component selection, safety considerations, and engineering validation.
