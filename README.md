# 🧠 Analog Layout Notes

A structured reference and study guide based on real-world IC layout experience across analog, memory (SRAM), SoC, and general physical design. Built for reflection, interview prep, and helping others avoid the pain of learning everything the hard way.

---

## 🧭 Layout Domains

### 🔌 Analog Layout
- Common centroid and interdigitated techniques
- Matching and symmetry considerations
- Guard rings, substrate contacts, and isolation
- ESD & latch-up protection strategies
- Handling high impedance and sensitive nodes

### 🧠 Memory Layout (SRAM)
- Bitcell placement and hierarchy
- Peripheral logic vs. memory core considerations
- Read/write assist circuits layout tips
- Margin-sensitive routing (low skew, low IR drop)
- Custom vs. compiler-generated layout integration

### 🧰 SoC Layout
- Integration of hard IP (PLLs, LDOs, ADC/DAC, etc.)
- Power grid planning, straps, and IR drop zones
- Clock tree and reset distribution best practices
- IO ring planning and padframe alignment
- Block-level vs. top-level LVS and DRC strategies

### 📏 General Layout Principles
- Matching, shielding, and symmetry fundamentals
- Dummy device usage and density rules
- Parasitics and coupling mitigation
- Analog/digital partitioning rules of thumb
- Floorplanning for reliability and performance

### 🛠️ Tools, Checks, and Sanity Tips
- Virtuoso and ICC2 layout tips
- LVS/DRC/PEX workflows
- EM/IR awareness at layout stage
- Integration pain points and workarounds

---

## 🧪 In Progress

This is a living notebook. More to come as I add past lessons, new insights, and layout patterns worth sharing.

