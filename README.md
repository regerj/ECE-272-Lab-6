# ECE 272 Section 6: Video Graphics Array (VGA)
### 6.1 Background Information
Video Graphics Array (VGA) can be used to display a wide range of resolutions and refresh rates. They draw lines left to right, top to bottom. Each pixel is controlled by 3 analog pins for Red, Green, and Blue (RGB). One common graphics mode is 640x480 at 60Hz. Modern VGA monitors are multi-sync so they are built to work with a range of frequencies. The two other pins that matter for controlling the image are Horizontal Sync and Vertical Sync. When Hysnc goes to 0, the next line starts to draw. When Vysnc goes to 0, it goes back to the top line again, starting a new frame.

<p align="center">
  <img width="550" height="400" src="https://github.com/regerj/ECE-272-Lab-6/blob/master/vgaconnections.png">
</p>

#### <div align="center">Figure 6.1: VGA pinout</div>

### 6.2 Section Overview
 

**Objective: Design and implement a system that generates the VGA outputs Hsync and Vsync, and properly controls the RGB values.**

* Create a software level block diagram for the design.
* Slow the 50MHz clock to 25Mhz.
* Generate the Hsync and Vsync Generator.
* Design logic to control the RGB values.
* Connect all modules together in the top level.
* Program and Test Hardware.
### 6.3 Learning Objectives
1. Learn how analog array video works.
2. Learn to generate timed signals.
### 6.4 Materials
1. Quartus Prime Lite Edition V. 18.0
2. DE10-Lite kit with MAX10 10M50DAF484C7G FPGA
3. USB to USB-B cable
### 6.5 Procedure:
#### <div align="center">There are 6 steps to digital logic design</div>

![Design Process Flow](https://github.com/regerj/ECE-272-Lab-4/blob/master/4.1%20Design%20Process.png)

#### <div align="center">Design Process Figure 6.2: Use this process for designing the final project.</div>

1. **Design:** The context of the design is established in this step. The context involves defining the inputs, desired outputs, and all the logic required in-between. In this step, all the minimizations and layout are planned for the design entry process. While this step is not always the longest, it should involve the most thought and effort. This typically requires a complete block diagram showing all the logic blocks and the connections between them, often with written explanations of specific functions.
2. **Design Entry:** The actual drafting of the digital logic design occurs in this step, translating the design from block diagrams and descriptions into the software. This can be accomplished directly by writing HDL code, or graphically by drawing a schematic that a software tool can convert into HDL code.
3. **Design Simulation:** Before committing to hardware, this step tests the design in a controlled computer simulation. If the design does not function as specified in the ”Design” step, it is revised.
4. **Synthesize and Map Design:** When the design simulates correctly, the HDL and schematic source files are synthesized into a design file that can be written to the FPGA. This includes assigning the inputs and outputs of the design to IO pins.
5. **Program Hardware:** After the design file is created, it is used to configure the FPGA. Quartus Prime sends a bit stream over the USB-B cable to configure the DE10-Lite FPGA.
6. **Test Hardware:** Verify hardware operation once the FPGA has been programmed. The FPGA should operate exactly as the design predicted, which was verified by the simulation. Synthesis problems, timing violations, or incorrect assumptions about the hardware can require the designer to return to the ”Design” step.
### 6.6 Design
You must design a system that generates the Hsync and Vsync signals with the correct timing. Each wave has 4 sections: Sync, back porch, display interval, and front porch (a,b,c,d, respectivly). Sync is the only time that the Hsync or Vsync signal is actually changed. It is driven low, and upon its rising edge the back porch starts. During both the back porch and the front porch, THE RGB VALUES MUST BE 0. Each Hsync makes a new line, each Vsync start the next frame by setting the line back to 0. You must keep track of the number of cycles and lines.

To do this,

1. Create a 25Mhz clock signal.
2. Design modules to: Count clock cycles, Generate (H/Z)Sync Signals, and Control the RGB

<p align="center">
  <img width="550" height="350" src="https://github.com/regerj/ECE-272-Lab-6/blob/master/vgahorizontaltimingspecification.png">
</p>

#### <div align="center">Figure 6.3 Horizontal Timing Specifications</div>

<p align="center">
  <img width="550" height="300" src="https://github.com/regerj/ECE-272-Lab-6/blob/master/vgatimingspecs.png">
</p>

#### <div align="center">Figure 6.4 Hsync and Vsync Tables</div>

<p align="center">
  <img width="550" height="300" src="https://github.com/regerj/ECE-272-Lab-6/blob/master/untitled_diagram_2.png">
</p>

#### <div align="center">Figure 6.5 Block Diagram</div>

### 6.7 Design Entry
Use Switches for the 2-bit RGB inputs.

Transcribe your block diagrams and logic into SystemVerilog. Connect it all together in the top level.

### 6.8 Design Simulation
It is highly recommended that use use ModelSim to simulate your design.

### 6.9 Test Hardware
Program the DE10_Lite and test the VGA output with a monitor.

### 6.10 Checkoff
* A software-level block diagram.
* A proper System Verilog Implementation of the Sync module.

* Valid hardware output
