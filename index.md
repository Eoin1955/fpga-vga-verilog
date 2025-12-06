---
layout: home
title: FPGA VGA Driver Project
tags: fpga vga verilog
categories: demo
---
## **Introduction**
This is the charmander pixelart that is made in verilog code that is displayed using a vga cable. It was made over 5 weeks where I started with color strips and learnt how to display an individual pixel to create pixel art.

## **VGA Design**
### **Project Set-Up**

The project setup was firstly made in the C temp file due to having errors when writing bitstream when the project is in onedrive. Using the Intellectual Property Wizard we generated a 25MHz clock speed from the already existing 100MHz clock from the board. In addition to the color stripes code I tested with, I added a Basys3 master constraint file to tie all files together. 

When using the orignal colourstripes code it showed vertical lines of different colours but in the setup I wanted to get more familiar with the code so I changed it to the background I was going to do as seen in the second image.

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/projectsummary.png">

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Background.png">


## **Summary of Project**
For the Structure we got was VGATop design source with vga sync, colour strips and where we added the clock wizard IP. Then the Basys3 master constraint file was added this brought all files togther. The testbench that includes VGASync and colour stripes.

VGA sync was used to produce the VGA timing signals; counting through all the horizontal and vertical pixels, including the porches for the vsync and hsync.

ColourStripes is the file that I changed to make my pixel art, it uses the 100MHz clock from the board, 10 wide bus input from row and col to then output a red, green and blue signal. Originally the code displayed simple vertical colour lines but now it produces the charmnder image.

### **Simulation**
The simulation was done by the built in simulator in vivado. The testbench simulated both VGASync and Colourstripes so that I could test different elements of my code. The timing of Hsync and Vsync pules and correct mapping between rows and columns and the rgb outputs can all be seen in this simulation of the project.

### **Synthesis**
Describe the synthesis and implementation processes. Consider including 1/2 useful screenshot(s). Guideline: 1/2 short paragraphs.

During Synthesis, Vivado changed the Verilog code into FPGA Logic, this logic mapped the design onto Look-Up tables, D flip-flops and routing on the Basys3's Artix-7 board. In the image below it shows the implemention of the clock wizard (that has a input of 100MHz and reset to output 25Mhz), vga sync (that has an input of 25MHz clk and rst to output a 10 bit bus column and row, hsync and vsync and vid_on that is the selectors for the multiplexers in vga red, blue and green), colour_stripes (with inputs from 100MHz clk, the 10 bit bus of row and column and rst. The colour stripes takes those inputs and then outputs the bluem green and red to go into their respective multiplexers) and the last three multiplexers of vga red, blue and green that takes the input from the colour stripes and a default 0 from ground and uses the vid_on selector to 
display the desired colour.

<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Elaborateddesign.png">



<img src="https://raw.githubusercontent.com/Eoin1955/fpga-vga-verilog/main/docs/assets/images/Implemention.png">



### **Demonstration**
Perhaps add a picture of your demo. Guideline: 1/2 sentences.

## **My VGA Design Edit**
Introduce your own design idea. Consider how complex/achievabble this might be or otherwise. Reference any research you do online (use hyperlinks).
### **Code Adaptation**
Briefly show how you changed the template code to display a different image. Demonstrate your understanding. Guideline: 1-2 short paragraphs.

### **Simulation**
Show how you simulated your own design. Are there any things to note? Demonstrate your understanding. Add a screenshot. Guideline: 1-2 short paragraphs.
### **Synthesis**
Describe the synthesis & implementation outputs for your design, are there any differences to that of the original design? Guideline 1-2 short paragraphs.
### **Demonstration**
If you get your own design working on the Basys3 board, take a picture! Guideline: 1-2 sentences.

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

