---
layout: page
title: Underwater ROV Design (MATE Competiton)
description: Robert College, October 2023 - June 2024
img:  assets/img/rov_welcome.jpg
importance: 3
category: Design & Prototyping
related_publications: false
---

**Role**: Team Lead (CEO), Mechanical Design, Integration

**Team**: Robert College Makers

**Competition**: MATE ROV World Championship 2024

**Award**: Co-recipient of the highest technical report score.

### Quick Highlights

- **Designed and manufactured a fully functional ROV with modular components**

- **Integrated 6-thruster hydrodynamic chassis, capable of autonomous operation.**

- **Developed and tested onboard control systems using Raspberry Pi & Pixhawk.**

- **Created a fully custom 3D-printed robotic arm with modular claw tips.**

### Project Overview

Aderone was the culmination of a year-long cycle of design, testing, and iteration as part of my high school robotics team. While I had spent several years working on ROVs, this final iteration stood out as our proudest success—earning an invitation to the MATE World Championship in Tennessee and tying for the highest technical report score.

The goal was ambitious: build an underwater robot capable of completing advanced tasks set by the MATE (Marine Advanced Technology Education) team like photogrammetry, coral transplanting, cable connection, and environmental sampling — all while staying compact, reliable, and adaptable to changing mission needs. (to learn more about the MATE ROV challenge visit their [website](https://materovcompetition.org/))

I served as CEO and worked cross-functionally across the design, electronics, software, and manufacturing domains – a role that required balancing leadership, hands-on problem solving, and a sharp eye for integration.

### Design Philosophy

The challenges set forth by the MATE team required various different tools to be utilized. There were times where the robot had to be precise with its movements gripping items like syringes, rocks, corals and there were times where the robot had to carry heavy loads and surface quickly. 

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/overview1.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/overview3.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/overview2.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
</div>
<div class="caption">
    Each year, MATE releases mission previews to clarify the tasks expected the vehicles to complete. These screenshots are taken from that overview.
</div>

Since the competiton rules dictate that all challenges can only be attempted in one go (no-breaks in between), the team decided early on that the best way to approach this problem was to build a vehicle that was very modular. This way the team could quickly use the downtime when the vehicle is surfaced to change tools and better approach all tasks. Furthermore given the time pressure to complete all tasks, the team decided a nimble vehicle would perform better.

Going into the design phase our objectives were clear:

- Modular, and quick change tooling components.
- Nimble but precise
- Hydrodynamic

The vehicle development was seperated in to three phases:

- Chasis Design and Manufacturing
- Electronics Integration & Tool Desing
- Pilot Tests & Autonomous Code Development

Since most of the development time also overlapepd with our high school responsiblities I have assigned an optimistic completion interval of two months per phase. This would give us enough time to double-check and trouble shoot any issues that might arise during the development project.

## Chasis Design and Manufacturing

In previous years designs we have utilized a bulky aluminium frame. While this allowed us to mount multiple tools and a larger electronics enclosure to the ROV, it made the vehicle very slow and not streamlined. Furhtermore due to the large footprint the vehicle often collided with other objects in the testing environment which was not ideal.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/tekno3.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="400px" %}
  </div>
</div>
<div class="caption">
    This was our previous year's design. A big studry aluminium frame paired with a large enclosure. Perfect for heavy duty applications.
</div>

In order to create a more streamlined chasis the team stripped the previous vehicle down to its essentials: 6 motors and a electronics enclosure. The motors were re-used from previous years design as they were powerfull and reliable and the electronics enclosure was swapped with a smaller alternative to decrease the overall front facing surface area of the vehicle. 

Instead of designing a chasis and then modifying it to mount these essentials, the team did the opposite and designed the chasis around these components. 

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/dev1.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
</div>
<div class="caption">
    This was the CAD preview of one of our refined designs for the front of the vehicle.
</div>

The chasis was split into three pieces: front, mid and back. These pieces were made by molding a rectangular block around the motors and the electronics enclosure. Once this initial stage was done the team used SolidWorks flow simulations to pinpoint areas of high drag and turbulance. The team iteratively refined these regions to get a shape that maximised flow efficiency.

Each adjustment translated to easier control, lower thruster load, and a faster response in water. Furthermore, the chasis being three seperate pieces meant the vehicle was very modular. Had a problem with the front? No problem just swap it out. The team also joined these pieces with four metal rods. These metal rods provided structural stability and also acted as mounting points for anything and everything you wanted the robot to carry: grippers, flashlights, cargo... 

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/showroom.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
</div>
<div class="caption">
    This was our initial prototype of the chasis built to verify dimensions and fits. We later painted it and made it a showroom vehicle. 
</div>

In order to capture the fine details and the true geomtery of the chasis the team decided the best manufacturing method would be 3D printing. The footprint was small enough to fit in a 256x256 bed and the structural requirements were way below the strength of the PLA material. Although it took some fine tuning to get the 3D printing just right, in the end our team was able to print the pieces with 100% infill to help with buoyancy.

<div class="row">
  <div class="col-sm mt-3 mt-md-0 text-center">
    {% include figure.liquid loading="eager" path="assets/img/MATE/printing.png" title="Task Previews" class="img-fluid rounded z-depth-1" width="600px" %}
  </div>
</div>
<div class="caption">
    The view from the 3D printer as the chasis pieces are being printed.
</div>

After printing and assembly, we performed weight and buoyancy analysis. By default, we aimed for neutral buoyancy—critical for minimizing vertical thruster load and maximizing control efficiency—but we intentionally tuned the balance slightly positive. This decision helped with payload tasks like lifting heavy props. The final tuning was done using foam inserts and small ballast weights, which were tested and swapped during field trials.

**Chasis Design and Manufacturing Summary**
- Compact, hydrodynamic, and modular chassis designed around core components

-Refined through flow simulation and 3D printed at high fidelity

- Tuned for neutral/slightly positive buoyancy using foam and ballast

## Electronics Integration & Tool Design

The previous years electronics were built for a much larger enclosure. The main challenge was adapting the same control system for this years design. There were also some changes to the electronics design from last year. The core components stayed the same, changes are marked in bold.

- Raspbery Pi 4 Running BluoOS developed by BlueRobotics for communication with ground computer and flight computer
- Pixhawk as a flight computer
- 12-5V Step Down Converter
- 6 ESCs to control the motors
- **2 Cameras (one facing front, one straight down towards the sea bed)**
- **3 Servo Controllers (one for camera tilt, and 2 for grippers or other tools)**

Last year we used a pnuematic system to actuate grippers. While this worked well, our team felt like it overcomplicated the design since a similar solution was available via waterproofed servo motors. Furthermore to aid the pilot the team wanted to use a extra camera.

Moreover previous years design had the motor cables inserted through cable penetrators to the watertight enclosure and then epoxied. This provided a great seal however it made diagnosing issues very hard because to access because the team had to juggle a large amount of wiring to reach the cause of the problem. To counteract this issue, the team opted to use waterproofed cable connectors on the outside of the ROV enclosure. This way the team was able to connect and disconnect the motor cables with ease and better troubleshoot the issue.

Trying to fit all these components in to a very small enclosure was a tough task but I was able to design a very compact solution without compramising safety.

!! show photo here showing the electronics enclosure

### Tool Design

In order to design the best tools for the challenges dictated by the MATE team we listed the motion capabilities required to complete the tasks:

- Pinching Motion
- Grab and Rotate
- Grab and Carry (for most of these tasks MATE provided hooks on the props to use while carrying)

At first we tried to combine all these functionalities to one single tool. However, we quickly realized it was way better to seperate the grabbing and pinching motions to two different tools. Since most of the stuff that was supposed to be carried had hooks attached to them for carry tasks we designed a tool that had a similar hook so that they would engage during the carrying process. For everything else we opted with a very simple design incorporating two straight blocks that were able to open and close in the shape of a V. (expand and fix)

(expand and fix) These grippers were attached to a servo that allowed it to open and close. In addition to this, the grip servo was connected to another servo which allowed the twisting motion required by the tasks. The system as a whole was attached to the metal rods that were used to connect the chasis together. 


**Electronics Integration & Tools Design Summary**
- 


## Pilot Tests & Autonomous Code Development
(expand and fix) It was hard to find a pool to let us use it for testing since most people were not comfortable letting us test while other people were using the pool.

(expand and fix) Contrary to our initial design beliefs the pilot tests quickly showed that the vehicle was too nimble. For most of the initial tests the pilot would miss the target and had a hard time alligning objects due to the very tuned responsivity and sensitivity of the vehicle. Thus the team had to contniously adjust motor power and input delay to make the vehicle more controllable. Neverthless, the initial tests showed promissing results with all systems and tools working as intended. 

(expand and fix) Another interesting thing we learned from the rigourous testing phase was the tool wear. Even though the servos we used were advertised as waterproof they would start exhibiting signs of water damage. When dissassembled the gears of the servos showed rusting and there were clear signs of moisture being present. Given our limited budget and limited waterproof servo suppliers available to us the team had to balance testing time with the potential risk of not having a servo by the time the competition rolls around.

(expand and fix) One of the mission objectives was to autonomously transport a coral piece to a designated area in red. The autonoumous part had to kick in after the vehicle grabs the coral. In order to tackle this problem our team begun training an image detection model using Yolov5. During one of our test dives we placed a red landing platform in water and took pictures from various angles to train the model. After the model was trained we used it to write a code that contiouslty tracked the red circle from the front camera intially. The robot moved forward to the red circle until it was visible from the downward facing camera and then the robot alligned itself using the downward facing camera. Once it was aligned the robot began to descend until it no longer saw the red circle or couldn't descend any further (as tracked by the gyro).

While this development was going steady and showed promissing signs our team unfortunatly had to abondon this part of our mission objective as the competition deadline was close and we felt like risking further wear in the pool was not worth it.


## Summary & Highlights




!! Pictures and videos from comp

