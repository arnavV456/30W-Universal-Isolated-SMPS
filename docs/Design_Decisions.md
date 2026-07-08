# Design Decisions

This document outlines the key engineering decisions made during the design of the **Universal 30W Isolated AC-DC Flyback Power Supply**.

---

# Why I Selected the MYRRA 74030 Transformer

The transformer is the heart of an isolated flyback converter, directly influencing efficiency, regulation, thermal performance, and electrical safety.

Instead of using an undocumented generic transformer, I selected the **MYRRA 74030** because it is a commercially manufactured transformer with published specifications, reinforced insulation, and documented electrical characteristics.

The transformer provides:

- 4 kV reinforced isolation
- 6 mm creepage distance
- Universal 85–265 VAC operation
- 30 W continuous power capability
- Published winding specifications
- Proven industrial reliability

Using a transformer with comprehensive manufacturer documentation significantly reduces design risk while improving reliability, repeatability, and long-term maintainability.

---

# Why I Chose the TOP244Y Controller

The **Power Integrations TOP244Y** was selected for its mature offline flyback architecture, integrated high-voltage power MOSFET, and extensive protection features. It is specifically designed for low-to-medium power isolated AC-DC converters operating from universal mains input.

Compared to discrete controller solutions, the TOP244Y significantly reduces component count while maintaining excellent reliability, efficiency, and electromagnetic compatibility.

Advantages include:

- Integrated 700 V power MOSFET
- Universal input (85–265 VAC) operation
- Built-in current limiting
- Thermal shutdown protection
- Soft-start functionality
- Reduced external component count
- Excellent EMI performance
- Proven industrial reliability

These features make it well suited for a compact, isolated 30 W flyback converter.

---

# Why the Flyback Output is 12V / 2.5A

The power supply is designed to deliver a regulated **12 V output capable of supplying up to 2.5 A**, allowing the converter to utilize the full capability of the selected transformer while providing additional flexibility for future applications.

The available output power is shared between:

- External 12 V loads
- On-board 5 V buck converter
- Conversion losses

Designing for the full **30 W** capability provides:

- Additional thermal margin during normal operation
- Greater flexibility for future applications
- Improved support for transient loads
- Better utilization of the transformer
- Lower component stress during typical operation

The 5 V rail is generated from the regulated 12 V output using a high-efficiency buck converter, allowing both outputs to share the available power while maintaining excellent regulation.

---

# Why Generate 5V Using a Buck Converter

Instead of designing a dual-output flyback converter with separate regulated secondary windings, the design regulates a single **12 V output** and derives **5 V** using a high-efficiency buck converter.

Advantages include:

- Better voltage regulation
- Improved cross-load performance
- Simpler transformer design
- Easier compensation
- Lower output ripple
- Reduced design complexity
- Easier debugging and validation
- Greater flexibility for future output voltages

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
| MOV | Suppresses mains surge voltages |
| NTC Thermistor | Limits inrush current during startup |
| Common-Mode Choke | Reduces conducted common-mode EMI |
| X-Class Capacitor | Suppresses differential-mode noise |
| Y-Class Capacitor | Suppresses common-mode noise while maintaining isolation |

Together, these components improve:

- Electrical safety
- Reliability
- Electromagnetic compatibility (EMC)
- Regulatory compliance

---

# Why Commercially Available Components Were Selected

Wherever possible, commercially available components with comprehensive documentation, established reliability, and long-term availability were selected.

Choosing components from established manufacturers provides several advantages:

- Published electrical characteristics
- Reliable thermal and safety performance
- Consistent manufacturing quality
- Long-term availability
- Easier sourcing and replacement
- Better confidence during design validation

Using well-documented components reduces engineering uncertainty and results in a more robust, maintainable, and reproducible design.

---

# Why the Flyback Topology Was Chosen

Among isolated converter topologies, the flyback converter provides the best balance of simplicity, cost, efficiency, and performance for power levels below approximately **50 W**.

Advantages include:

- Single magnetic component
- Galvanic isolation
- Universal input capability
- Low component count
- Compact PCB footprint
- Mature design ecosystem
- Excellent efficiency in the 20–30 W range
- Wide availability of compatible components

For a universal-input **30 W** AC-DC power supply, the flyback topology provides an ideal balance between performance, manufacturability, reliability, and design complexity.

---

# Project Design Philosophy

The objective of this project is not simply to produce a functioning power supply, but to develop a **professionally engineered offline switch-mode power supply** following industry-standard engineering practices.

The project emphasizes:

- Reliability over minimum cost
- Careful component selection
- High-voltage PCB layout best practices
- Proper creepage and clearance
- Robust thermal performance
- EMI-conscious design
- Comprehensive documentation
- Reproducible engineering decisions

Every major design decision is documented and justified to ensure the final hardware is maintainable, safe, and technically sound.

The completed project is intended to demonstrate practical skills in:

- Offline AC-DC power supply design
- Flyback converter implementation
- High-voltage PCB layout
- Isolation and safety engineering
- Component selection
- Power electronics
- Hardware validation and testing
- Engineering documentation

The goal is to produce a power supply that is not only functional, but also representative of professional engineering practices used in commercial embedded and industrial power electronics.
