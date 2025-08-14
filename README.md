# IC Layout Notes

A structured reference and study guide drawn from real-world IC layout experience across analog, memory (SRAM), SoC, and general physical design. Built for reflection, interview prep, and helping others avoid the pain of learning everything the hard way.

---

## Layout Domains

### Analog Layout
Analog layout quality directly impacts performance, matching, and yield. Even with the best schematic, careless layout can destroy circuit precision.  

- [Analog Layout Interview Questions](./analog_layout_interview_questions.md) — Common interview prep topics and concept checks.  
- [Analog Block Glossary](./analog_block_glossary.md) — Descriptions of common analog building blocks.

**Core principles to remember:**
1. **Matching & Symmetry** — Matched devices should share identical surroundings: same distance to wells, same STI boundaries, mirrored guard rings.
2. **Placement Techniques** — Use *common-centroid* or *interdigitated* arrangements to average out gradients and stress effects.
3. **Guard Rings & Isolation** — Surround sensitive devices with mirrored guard rings; ensure equal proximity on all sides to avoid imbalance.
4. **ESD & Latch-up Prevention** — Follow foundry guard ring/tap spacing rules to protect inputs and maintain substrate bias control.
5. **Sensitive Node Handling** — Shield high-impedance nodes from noisy routing and keep them short to minimize parasitic coupling.

---

### Memory Layout (SRAM)
SRAM layout requires strict adherence to foundry design rules and careful integration with peripheral circuitry. The bitcell array itself is fixed, but the surrounding design determines performance, power, and yield.

**Core principles to remember:**
1. **Bitcell Placement** — The core array is fixed; never alter its geometry. Focus on precise integration with the periphery.
2. **Periphery vs. Core** — Periphery devices (sense amps, write drivers, assist circuits) can use analog matching techniques, while the core must remain rule-driven.
3. **Routing for Performance** — Keep bitlines and wordlines short and balanced to reduce skew and IR drop.
4. **Assist Circuits** — Lay these out to minimize coupling into sensitive lines, maintaining symmetry for consistent performance.
5. **Custom vs. Compiler-Generated** — Know how each integrates at top level and its impact on IR drop, skew, and verification.

**Practical tip:** Apply analog layout best practices to the periphery while treating the core as untouchable.

---

### SoC Layout
System-on-Chip (SoC) layout involves integrating multiple IP blocks into a unified design while meeting performance, power, and reliability targets. The challenge is balancing signal integrity, manufacturability, and complex physical constraints.

**Core principles to remember:**
1. **Hard IP Integration** — Place sensitive analog and mixed-signal IPs (PLLs, LDOs, ADC/DACs) with adequate isolation from noisy digital regions.
2. **Power Grid Planning** — Ensure robust strap placement and via density to minimize IR drop and electromigration risks across the chip.
3. **Clock & Reset Distribution** — Design early for balanced clock tree and reset paths to avoid skew and timing closure surprises.
4. **I/O Ring & Padframe** — Align pads for manufacturability and ESD protection while maintaining consistent pad-to-core routing.
5. **Verification Strategy** — Plan for both block-level and top-level LVS/DRC from the outset to prevent integration bottlenecks.

**Practical tip:** Lock down power and clock distribution before fine-tuning signal routes.

---

## General Layout Principles
These rules apply to all layout domains and form the foundation of good physical design. They help maintain performance, matching, and manufacturability across different process nodes.

**Core principles to remember:**
1. **Symmetry First** — In matched devices, maintain mirrored geometry, routing, and surroundings to cancel out process gradients and stress effects.
2. **Layout Dependent Effects (LDE)** — Control well proximity, STI stress, and diffusion effects by keeping device environments balanced.  
   See: [Layout Dependent Effects (LDE)](./layout-dependent-effects.md)
3. **Density & Dummy Devices** — Use dummy gates, diffusion, and fill to meet local density targets and avoid CMP-induced variation.
4. **Shielding & Parasitics** — Place grounded shields between sensitive nodes and aggressors; keep critical nets short to minimize coupling.
5. **Partitioning** — Separate analog and digital regions to reduce substrate noise, clock interference, and thermal gradients.
6. **Floorplanning for Reliability** — Consider electromigration, IR drop, and ESD paths early in the design to avoid last-minute redesigns.

**Practical tip:** If symmetry is broken, expect performance drift — fix it at layout, not in post-silicon debug.

---

## Tools, Checks, and Sanity Tips
Efficient layout work depends on knowing your tools, verifying early, and avoiding common late-stage issues.

**Core principles to remember:**
1. **Tool Mastery** — Learn productivity shortcuts in Virtuoso and ICC2; configure views and layers to highlight rule-sensitive areas.
2. **Verification Workflow** — Run LVS, DRC, and PEX incrementally instead of waiting until the end of a block or chip.
3. **EM/IR Awareness** — Use analysis tools during layout, not just at sign-off, to catch early power and reliability issues.
4. **Automation** — Use scripts or built-in automation to check repetitive layout patterns, density, and via rules.
5. **Peer Reviews** — Have another layout engineer scan for symmetry, shielding, and spacing violations before formal verification.

**Practical tip:** Treat verification like layout’s second half — start it as soon as possible and run it often.
