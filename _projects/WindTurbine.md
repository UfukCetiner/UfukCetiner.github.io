---
layout: page
title: Small Scale Wind Turbine Blade Design
description: Imperial College, Year 1, Summer Term Project, June 2025
img: assets/img/windturbineblade_final.jpg
importance: 1
category: Design & Prototyping
related_publications: false
---
The goal of this project was to design and manufacture small scale wind turbine blades with a group of 6. The project constraints were as follows:

- Must be a horizontal axis wind turbine (HAWT)
- Max Turbine Diameter: 0.5 m
- Self-Starting Speed: 10 m/s
- Must rotate clockwise when viewed from wind direction
- Turbine must be upwind of the tower

In addition to these initial considerations, teams faced further manufacturing and budget constraints. Each group was allocated a total budget of £100 and was limited to specific manufacturing techniques and materials. Only laser cutting and 3D printing were permitted—laser cutting was free, while 3D printing cost £5 per hour for the first 3 hours and £25 per hour thereafter. The approved materials included plywood, balsa wood, acrylic, tough PLA, carbon fiber strips, epoxy, and steel rods. However, the use of epoxy or any other adhesives as fillers or mold materials was strictly prohibited.

Given these constraints, teams were tasked with designing blades capable of generating maximum power through aerodynamic analysis and structural calculations. The teams had three weeks to finalize their designs, after which no modifications were allowed during the manufacturing phase (2 weeks).

Our team was divided into three sub-teams: Aero, Structures, and CAD/Manufacturing. While my primary role was within the CAD/Manufacturing group, I also contributed to the aerodynamic design efforts. The following is a comprehensive account of our team's work throughout the project.

# Aerodynamic Calculations

The Blade Element Momentum (BEM) theory was used to estimate the performance of the wind turbine blades. BEM combines blade element theory with momentum theory to calculate the forces on each blade section by dividing the blade into small elements and evaluating local flow conditions. From this, the total thrust and torque can be computed, and subsequently, the power output of the turbine. Accurate performance prediction with BEM requires reliable airfoil polar data (typically lift and drag vs. angle of attack) for each blade section, as these values directly influence the force calculations at each element. To improve the fidelity of the model, several correction factors were applied: the Prandtl tip loss correction accounts for the reduction in lift near the blade tip due to finite span effects; the tangential induction factor (a’) adjusts for angular momentum extraction; the root-loss correction models losses near the blade hub; and the stall delay correction accounts for delayed flow separation on rotating blades. 

The airfoils used in the blade design were selected based on literature specific to low Reynolds number performance in small-scale wind turbines. The SG (Selig) family of airfoils, particularly designed for low-speed applications, has been highlighted in multiple academic sources for their high aerodynamic efficiency. Among these, the SG6043 stood out due to its high CL/CD​ ratio across a wide angle-of-attack range, making it an excellent candidate for maximizing power output in moderate wind conditions.

However, integrating the SG6043 directly at the blade root posed significant structural challenges. Our initial prototypes revealed that the abrupt geometric transition from a thick circular root (necessary for mounting and load transfer) to the thin trailing edge of the SG6043 introduced high stress concentrations and manufacturing difficulties. To address this, we implemented a gradual geometric transition using a sequence of NACA 4-digit airfoils: NACA 4424, NACA 4420, and NACA 4416, tapering smoothly into the SG6043 at the outer blade span. This not only reduced structural stress at the critical root region but also improved manufacturability and load distribution along the blade.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/thickness_problem.jpg" title="Initial Blade w/o Transition" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
</div>
<div class="caption">
    This was an initial look at the blade design. Without the transition region aerofoils, the blade suffered from a sharp transition from the thick circular root. 
</div>

To run Blade Element Momentum (BEM) calculations with these airfoils, the team generated the necessary aerodynamic polars using XFOIL, a widely used panel method tool for low-Re simulations. These CL​ and CD​ vs. angle-of-attack curves provided the core input for our BEM performance model, enabling force and power predictions across varying operational conditions. While XFOIL provided a fast and accessible way to generate polar data, its accuracy at very low Reynolds numbers and post-stall behavior remains limited — something we would come to realize during post-testing analysis.

### Twist and Chord Distributions
One of the key aspects of aerodynamic blade design is defining the twist and chord distributions along the blade span. Because the tangential velocity increases with radius, each airfoil section along the blade operates at a different local flow angle. The twist distribution compensates for this by adjusting the local pitch of the airfoil, ensuring each section operates near its optimal angle of attack — as determined from the CL​/CD​ trends in the XFOIL-generated polars.

To calculate the ideal twist and chord, our team initially used analytical relationships derived from Glauert's optimum rotor theory, which assumes maximum power extraction under ideal (Betz-optimal) conditions. These equations distribute twist inversely with radius and produce high chord values near the hub where wind speed is low but torque production is critical. However, in practice, the resulting bulky root sections posed significant challenges: they were difficult to transition into from the circular hub geometry, required large amounts of material, and were not easily manufacturable within the given manufacturing constraints.

To mitigate this, we turned to academic studies focused on small-scale turbine manufacturing. One particularly insightful recommendation was to begin linearizing the twist and chord distributions starting from 70–90% of the blade span — essentially tapering the aerodynamic sections smoothly into a structural root. This method simplifies both geometry and material usage, while maintaining acceptable aerodynamic performance. Our team adopted this approach, introducing a gradual transition from the aerodynamic SG6043 profile into more robust NACA sections, and eventually to a circular root profile.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/idealvslinearized.jpg" title="Ideal vs Linearized" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
    These graphs show the ideal vs linearized chord and twist distributions. The linearized distributions are the ones our teams used in manufacturing the blade.
</div>

This adjustment greatly reduced material cost and manufacturing complexity, which we considered a major win at the time. Interestingly, simulations showed no drop in predicted performance — in fact, the linearized design outperformed the theoretical optimum in our model, which in hindsight should have raised some eyebrows.

Looking back, one of our key oversights was placing too much trust in the research paper we referenced. While linearizing the chord distribution can be physically justified — as it primarily affects surface area and loading distribution — linearizing the twist lacks a solid aerodynamic basis. Twist is directly tied to the inflow angle experienced by each blade section, which depends on local blade speed and wind velocity. Deviating from the ideal twist essentially shifts the operating point away from the airfoil’s optimal AoA. This subtle but important difference wasn’t fully appreciated at the time.

It's likely that limitations in our simulation pipeline, especially the use of XFOIL at very low Reynolds numbers, further masked the aerodynamic penalties of the twist approximation. But in the excitement of simplifying the design and making visible progress, we didn’t stop to question whether those gains were real — or just numerical illusions.

### Starting Torque: The Critical Oversight

A final but crucial consideration in the aerodynamic analysis of the blade is its starting torque. Unlike steady-state conditions, real-world wind turbines must overcome the initial resistive torque of the generator — in our case, a small dynamometer — from complete rest. This means the blades must extract rotational energy from low-speed wind even when their angular velocity is zero.

Our BEM analysis estimated a starting torque approximately double the dyno’s resistive torque. Encouraged by this safety margin of two, we concluded that the turbine would reliably self-start under expected wind conditions. Since starting torque is strongly influenced by the root chord length, and our simulations showed favorable results, we opted not to modify the geometry further.

However, in testing, the turbine failed to self-start entirely. This was a key moment of realization: our confidence in the starting torque predictions had been based on overly optimistic input data — particularly the airfoil polars generated by XFOIL, which are known to underpredict stall and overestimate lift at very low Reynolds numbers. In addition, our “safe” factor of two left little room for real-world uncertainties like frictional losses, turbulent gusts, and delayed flow development at startup.

In hindsight, we underestimated the critical role of starting torque in small-scale turbine performance. A more conservative approach would have been to run BEM simulations at lower wind speeds to assess startup performance under more challenging conditions. Verifying that the turbine could overcome resistive torque in weaker winds would have provided an extra layer of safety margin, and likely would have exposed the overconfidence in our model far earlier in the process.

Instead, we learned (the hard way) that startup dynamics deserve just as much attention as peak efficiency in practical blade design.

## 🧠 Lessons Learned

- **Don't trust simulation results blindly** — validate them using experimental data.
- **XFOIL can be misleading** at low Reynolds numbers.
- **Linearizing twist isn't physically justified** — chord, yes; twist, no.
- **Starting torque needs aggressive safety margins** — theory alone won’t make a blade spin.


# Structural Calculations

In parallel with the aerodynamic design, other members of the team conducted a detailed structural analysis to ensure the blade could withstand operational loads without compromising performance.

Using MATLAB, the structural group estimated aerodynamic loading along the blade span (based on BEM results) and applied the shoelace formula to calculate cross-sectional areas for each blade segment. These areas were used to compute bending moments, and the resulting Von Mises stresses were evaluated — including contributions from centrifugal forces due to rotation.

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/structures1.jpg" title="Top Stress Distro" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/structures2.jpg" title="Bottom Stress Distro" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
    These figures show the stress distributions on the top and bottom surface of our blade. 
</div>

To guide material selection, the team compared the calculated stresses against allowable values for different candidate materials. Plywood was ultimately selected for its balance of structural strength, manufacturability, and cost-effectiveness. Blade deflections under load were also assessed to ensure that deformation would not significantly alter the airfoil geometry and affect aerodynamic performance.

Additionally, the team evaluated the adhesive strength of wood glue versus epoxy, a decision that later influenced the manufacturing process to ensure the integrity of the blade bonding under operational stresses.


# Final Design : Post Aero & Structural Analysis

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid 
       loading="eager" 
       path="assets/img/bladeFresh.jpg" 
       title="Blade geometry out of aero and structural analysis" 
       class="img-fluid rounded z-depth-1" 
       width="550px" 
    %}
  </div>
</div>

<div class="caption text-center mt-2">
  This was our final blade geometry after aero and structural analysis. At the time it predicted good performance and structural strength.
</div>

# Manufacturing
Given the manufacturing constraints, the team evaluated several options for blade manufacturing. 3D printing was quickly ruled out due to its high cost. Instead, we agreed on a more economical and scalable approach: laser-cutting blade cross-sections from plywood and stacking them to form the final geometry.

There were two feasible slicing strategies:
- Slicing along the x-axis, creating airfoil-shaped layers
- Slicing along the z-axis, producing thin spanwise sections

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/z-axis.jpg" title="Sliced across the z-axis" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/x-axis.jpg" title="Sliced across the x-axis" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
    These were the two options we considered when deciding the manufacturing method.
</div>

After weighing in pros and cons from both options, the team chose the z-axis slicing technique. This approach had two major advantages: it required fewer total sections, reducing both cutting and assembly time, and it allowed for more accurate representation of twist and chord variations along the blade span. More importantly it enabled us to orient the grain direction of the plywood perpendicular to the main aerodynamic loads which increased the blade's strength and safety margin by aligning the material’s strongest axis with the dominant bending stresses.

Each section was laser cut from 0.8 mm plywood to capture fine geometric detail. We also added engraved outlines and internal alignment markers to ensure the layers stacked with consistent orientation and minimal deviation during assembly.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/engraved1.jpg" title="Outlines showing engraving lines" class="img-fluid rounded z-depth-1" width="350px" %}
  </div>
</div>
<div class="caption">
    See the engravings of the outlines of the sections in blue. This allowed us to glue the sections like puzzle pieces.
</div>

Once the sections were stacked and glued, the team began the sanding process to refine the outer surface. To avoid over- or under-sanding, custom curvature guides were laser cut at various points along the span. These guides matched the intended airfoil shapes at specific blade stations, allowing us to check the blade’s profile during sanding and ensure adherence to the intended aerodynamic shape.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/sanding_before after.jpg" title="Outlines showing engraving lines" class="img-fluid rounded z-depth-1" width="350px" %}
  </div>
</div>
<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/fitcheck.jpg" title="Outlines showing engraving lines" class="img-fluid rounded z-depth-1" width="550px" %}
  </div>
</div>
<div class="caption">
    Images from the sanding process.
</div>

The test turbine hub featured a dovetail slot, which required precise interfacing geometry. To adapt the blade to this mounting system, the team designed a custom hub attachment piece. This component featured complex geometry and tight tolerances — particularly at the dovetail interface — making it an ideal candidate for 3D printing.

The attachment was printed with two countersunk holes to accept wood screws, serving as the primary mechanical fastening method. For additional strength and to improve the joint’s durability under load, the team also applied epoxy at the interface between the hub piece and the blade root.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/dovetail.jpg" title="Dovetail joint." class="img-fluid rounded z-depth-1" width="250px" %}
  </div>
</div>
<div class="caption">
    The dovetail joint to the main blade using epoxy and wood screws.
</div>

After assembly, the blades were sanded down once more to ensure a smooth aerodynamic surface. To avoid rotor imbalance, the final blade weights were matched to within 1% of each other. This small mass tolerance was critical to maintaining stability at operating speeds.

Finally, we applied a varnish coating to seal the surface, strengthen the plywood’s grain, and give the blades a smooth, durable finish.

# Conclusion

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/bladefin.jpg" title="Finished Blade" class="img-fluid rounded z-depth-1" width="250px" %}
  </div>
    <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/windturbineblade_final.jpg" title="Finished Blade" class="img-fluid rounded z-depth-1" width="250px" %}
  </div>
</div>
<div class="caption">
    The finished blades!
</div>

This project was more than just a design-build-test exercise — it was a deep dive into real-world engineering. From aerodynamic modeling and structural analysis to laser-cut manufacturing and iterative testing, it challenged me to apply theory in tangible, often unpredictable ways.

Some parts went remarkably well. The blade came out precisely manufactured, lightweight, and balanced. Clever decisions — like aligning plywood grain with aerodynamic loading and using transition airfoils to ease structural stress — paid off in fabrication and form. On the other hand, overly optimistic assumptions in simulation led to a blade that didn’t self-start, revealing just how fragile performance predictions can be when models aren't stress-tested.

That experience taught me to be skeptical of “perfect” outputs, to question inputs more critically, and to design with margin — especially when working at low Reynolds numbers or with experimental data like XFOIL.

It also sharpened my ability to collaborate across domains, prototype quickly, and adapt designs under constraints. Above all, it reminded me that setbacks aren’t failures — they’re feedback. And I’m genuinely proud of both the outcome and the learning curve behind it.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid 
       loading="eager" 
       path="assets/img/homage1.jpg" 
       title="Sliced across the z-axis" 
       class="img-fluid rounded z-depth-1" 
       style="height: 300px; object-fit: contain;" 
    %}
  </div>
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid 
       loading="eager" 
       path="assets/img/homage2.jpg" 
       title="Sliced across the x-axis" 
       class="img-fluid rounded z-depth-1" 
       style="height: 300px; object-fit: contain;" 
    %}
  </div>
</div>
<div class="caption">
    Some memories from the workshop.
</div>
