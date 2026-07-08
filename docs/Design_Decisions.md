Why I selected the MYRRA 74030 transformer

The transformer is the most critical component in an isolated flyback converter, influencing efficiency, regulation, thermal performance, and safety. Instead of using an undocumented generic transformer, I selected the MYRRA 74030 because it is a commercially manufactured transformer with published winding information, reinforced insulation, and documented compatibility with several offline flyback controllers. The transformer provides 4 kV isolation, 6 mm creepage, and is designed for 85–265 VAC offline applications up to 30 W, making it well suited for a 24 W design. Using a transformer with manufacturer documentation significantly reduces design risk and improves confidence in long-term reliability.

Why I chose the TOP244Y controller

Rather than using a low-cost controller with limited application documentation, I selected the TOP244Y because it is supported by extensive reference designs, application notes, and proven commercial implementations. The MYRRA 74030 transformer is specifically listed as compatible with the TOP244Y for 85–265 VAC operation, allowing the design to build upon a validated ecosystem instead of reverse-engineering an undocumented solution. This approach improves reliability, simplifies debugging, and results in a more professional design.

Why the flyback output is 12 V / 2 A

Although the original requirement was 12 V @ 1 A and 5 V @ 1 A, both outputs may be required simultaneously. Since the 5 V rail is generated from the 12 V rail using a buck converter, the flyback stage must supply both the external 12 V load and the power consumed by the buck converter.

Designing the flyback for 12 V @ 2 A (24 W) provides sufficient power for:

12 V external load
5 V buck converter
Conversion losses
Startup transients
Thermal derating

Operating the 30 W transformer below its maximum rating also improves reliability and reduces operating temperature.

Why generate 5 V using a buck converter

Instead of designing a multi-output flyback with independent 5 V and 12 V secondary windings, I chose to regulate a single 12 V output and derive 5 V using a synchronous buck converter.

Advantages include:

Better voltage regulation
Improved cross-load performance
Simpler transformer design
Easier feedback compensation
Lower output ripple
Reduced design complexity

Since modern buck converters typically achieve efficiencies above 90%, the additional conversion stage has minimal impact on overall system efficiency while greatly improving regulation.

Why reinforced creepage and isolation were used

This power supply is directly connected to the AC mains and therefore requires proper electrical isolation between the primary and secondary circuits.

The PCB is designed with:

Reinforced isolation barrier
Minimum 6 mm creepage
Isolation slot beneath the transformer and optocoupler
Separate primary and secondary copper pours
No routing across the isolation barrier

These measures reduce the risk of dielectric breakdown and improve electrical safety during long-term operation.

Why input protection components were included

An offline AC-DC power supply is exposed to surges, inrush current, and electrical noise from the mains supply.

The input stage therefore includes:

Fuse – protects against catastrophic faults.
MOV – suppresses mains surge voltages.
NTC thermistor – limits inrush current when charging the bulk capacitor.
Common-mode choke – reduces conducted EMI.
X-class safety capacitor – suppresses differential-mode noise.
Y-class safety capacitor – provides a controlled return path for common-mode noise while maintaining isolation.

These components improve safety, reliability, and electromagnetic compatibility.

Why I used a commercially available transformer instead of designing my own

Designing a flyback transformer requires detailed magnetic design, core selection, winding calculations, insulation design, leakage inductance optimization, and validation under varying operating conditions.

For this project, I intentionally chose a commercially manufactured transformer to focus on the design of the complete power supply while relying on a transformer with documented characteristics and safety approvals. This approach reflects common industrial practice, where engineers often build products around qualified magnetic components rather than designing custom transformers unless high-volume production justifies the additional development effort.

Why this topology was chosen

Among isolated converter topologies, the flyback converter offers the best balance of simplicity, cost, and performance for power levels below approximately 50 W.

Advantages include:

Single magnetic component
Galvanic isolation
Wide input voltage capability
Low component count
Compact PCB footprint
Mature design ecosystem
Good efficiency in the 20–30 W range

For a universal-input 24 W power supply, the flyback topology provides an excellent compromise between complexity and performance.
