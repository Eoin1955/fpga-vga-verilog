---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---
## **Introduction**
This is the charmander pixel art that is made in verilog code that is displayed using a vga cable. It was made over 5 weeks where I started with color stripes and learnt how to display an individual pixel to create pixel art.

## **VGA Design**
### **Project Set-Up**

The project setup was firstly set up in the C temp folder due to having errors when writing bitstream when the project is in OneDrive. Using the Intellectual Property Wizard we generated a 25MHz clock speed from the already existing 100MHz clock from the board. In addition to the color stripes code I tested with, I added a Basys3 master constraint file to tie all files together. 

When using the original colourstripes code it showed vertical lines of different colours but in the setup, I wanted to get more familiar with the code so I changed it to the background I was going to do as seen in the second image.

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/projectsummary.png">

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Background.png">


## **Summary of Project**
The Structure we were given included VGATop design source with vga sync, colour stripes and where we added the clock wizard IP. Then the Basys3 master constraint file was added this brought all files together. The testbench that includes VGASync and colour stripes.

VGA sync was used to produce the VGA timing signals; counting through all the horizontal and vertical pixels, including the porches for the vsync and hsync.

ColourStripes is the file that I changed to make my pixel art, it uses the 100MHz clock from the board, 10-bit bus input from row and col to then output a red, green and blue  signal. Originally the code displayed simple vertical colour lines but now it produces the charmander image.

### **Simulation**
The simulation was done by the built-in simulator in vivado. The testbench simulated both VGASync and ColourStripes so that I could test different elements of my code. The timing of Hsync and Vsync pulses and correct mapping between rows, columns and RGB outputs can all be seen in this simulation of the project.

### **Synthesis**
During Synthesis, Vivado changed the Verilog code into FPGA Logic, this logic mapped the design onto Look-Up tables, D flip-flops and routing on the Basys3's Artix-7 board. In the image below, it shows the implemention of the clock wizard (that has a input of 100MHz and reset, and outputs 25Mhz), vga sync (that has an input of 25MHz clk and rst to output a 10-bit bus column and row, hsync and vsync and vid_on that is the selectors for the multiplexers in vga red, blue and green), colour_stripes (with inputs from 100MHz clk, the 10 bit bus of row and column and rst. The colour stripes takes those inputs and then outputs the bluem green and red to go into their respective multiplexers) and the three VGA output multiplexers of vga red, blue and green that takes the input from the colour stripes and a default 0 from ground and uses the vid_on selector to display the desired colour.

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Elaborateddesign.png">


In the image below it shows the implementation stage this is when the translated verilog code is routed and placed onto the physical board. Each turquoise block represents a logic element such as LUTs, flip-flops and different routing resources. Vivado placed the elements in a compact area because the design is lightweight, the routing is done easier with more of the components being in one area on the board.

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Implemention.png">

### **Demonstration**
The first image below is the progress made in week 2 of this mini project. From the start where I had just the background I got to understand verilog code a lot more to better advance my design.
<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/partwaydone.png">

The second image is the completed pixel art of the pokemon charmander. This project helped me understand Hsync, Vsync, Lookup tables, multiplexers, Vga connectors better and verilog.
<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/complete.png">

## References

[1] Basys 3 reference manual
https://digilent.com/reference/programmable-logic/basys-3/reference-manual

[2] AMD synthesis introduction
https://docs.amd.com/r/en-US/ug901-vivado-synthesis/Introduction?
tocId=kZooy_YPGXnOJ6cjeLvz2A

[3] VGA signal timing
http://tinyvga.com/vga-timing/640x480@60Hz




<!--## **More Markdown Basics**
This is a paragraph. Add an empty line to start a new paragraph.

Font can be emphasised as *Italic* or **Bold**.

Code can be highlighted by using `backticks`.

Hyperlinks look like this: [GitHub Help](https://help.github.com/).

A bullet list can be rendered as follows:
- vectors
- algorithms
- iterators

Images can be added by uploading them to the repository in a /docs/assets/images folder, and then rendering using HTML via githubusercontent.com as shown in the example below.

<img src="https://raw.githubusercontent.com/melgineer/fpga-vga-verilog/main/docs/assets/images/VGAPrjSrcs.png">-->

