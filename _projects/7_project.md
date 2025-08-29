---
layout: page
title: Gate-Level Design of an 8-Bit Von Neumann CPU
description: Complete 8-bit processor built at the gate level
img: assets/img/cpuu.jpg
importance: 1
category: work
display_categories: ["work", "Academic"]
related_publications: false
---

A fully functional <strong>8-bit CPU</strong> designed from scratch based on the Von Neumann architecture.  
The processor integrates all fundamental components — including datapath, memory, control logic, and an arithmetic logic unit — constructed at the gate level without high-level abstractions.  

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/ControlUnit.jpg" title="Control Unit" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Adder8Bit.jpg" title="8-Bit Adder" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Register.jpg" title="Register Design" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The complete system combines the <strong>control logic</strong>, <strong>arithmetic unit</strong>, and <strong>register modules</strong>.  
    A common 8-bit data bus interconnects all subsystems, enabling seamless transfer of instructions and data between memory, the ALU, and registers.  
</div>

---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/CPU.jpg" title="CPU Top-Level View" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Top-level schematic of the processor showing the datapath, memory, and program control units working together.  
    The modular structure ensures each block — from instruction register to RAM — can be tested and integrated independently.  
</div>

---

<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/ALU.jpg" title="Arithmetic Logic Unit" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/FullAdder.jpg" title="Full Adder Detail" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The <strong>Arithmetic Logic Unit</strong> supports eight arithmetic and logical operations, with carry-out and zero flags for conditional branching.  
    At its core lies a gate-level <strong>full adder</strong>, which serves as the building block for multi-bit operations.  
</div>

---
