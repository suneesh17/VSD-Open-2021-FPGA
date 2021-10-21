# VSD-Open-2021-FPGA-Tutorial

![137896513-0cc9dace-0454-43a7-be28-a6ce883cf631](https://user-images.githubusercontent.com/72123647/138161674-73cbdebe-5568-4381-9a06-f23f427a780f.png)

This repository contains the documentation of the tutorial on "Digital Design on FPGA", an online workshop conducted by VLSI System Design (VSD)

## Table of Contents
- [`Introduction`](#introduction)
- [Interfacing LEDs](#interfacing-leds)
- [LED Counter](#led-counter)
- [Seven Segment Display](#Seven-Segment-Display)
- [4-way Traffic Light Controller](#4-way-Traffic-Light-Controller)
- [References](#references)
- [Author](#author)
- [Acknowledgement](#acknowledgement)


  
## Introduction

### 1. FPGA

 Field Programmable Gate Array (FPGA) are ICs that allows the hardware designer to program the device to perform an operation for a specific application. The term Field Programmable itself means that the IC is not fixed at the time of manufacturing but rather user defined. It is mainly used as a prototype for ASICs.
 
### 2. Verilog
  
  Verilog, a Hardware Description Language (HDL), used for describing a digital system in a more robust and flexible way. This is achieved when it creates a level of abstraction to hide away the implementation details.
  
### 3. Makerchip

  A free web based IDE for developing  high quality integrated circuits. It allows us to code, compile, simulate and debug verilog designs, all from your browser. Makerchip is also available as an app on all OS platforms.
  For more information, visit: https://www.makerchip.com/

# Interfacing LEDs
  In this section, we deal with interfacing of LEDs by simulating them on the virtual FPGA board by using System Verilog.
  
  Refer to the link for the project:
  https://makerchip.com/sandbox/0VOflhxZZ/0Anh1Zw#
### a. Code
```
\m4_TLV_version 1d: tl-x.org
\SV
	m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
	//Author- SUNEESH HARAN
	wire [7:0] leds;
	//assign leds= 8'b11010110;
	//assign leds= 8'b11100101;                   
	                   
		                   
   // write your code here
   
\TLV
   // M4_BOARD numbering
   // 1 - Zedboard
   // 2 - Artix-7
   // 3 - Basys3
   // 4 - Icebreaker
   // 5 - Nexys
   m4_define(M4_BOARD, 1)
   m4+fpga_init()
   m4+fpga_led(*leds)
\SV
   endmodule
   ```
   
### b. FPGA Board output

![snap1](https://user-images.githubusercontent.com/72123647/138233258-d3ef440a-3e88-4f79-8ba0-d7e10002c4b1.PNG)

![snap2](https://user-images.githubusercontent.com/72123647/138234574-0ee2b8c2-d764-476c-a976-9dd97005005f.PNG)


### c. Diagram
  
 ![snap3](https://user-images.githubusercontent.com/72123647/138235814-7063f87a-8e69-4f3d-b05f-b427b89b253e.PNG)


### d. Waveform

  ![snap4](https://user-images.githubusercontent.com/72123647/138236013-a73c94d0-34dd-44f6-89c1-db44f112f646.PNG)

# LED Counter

  In this section, we deal with LED counter. We simulate them on the Virtual FPGA Board using System Verilog.
 
  Refer to the link for the project: https://makerchip.com/sandbox/0VOflhxZZ/0DRhOjK
  
  ### a. Code
  ```
  \m4_TLV_version 1d: tl-x.org
\SV
	m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
   reg [7:0] led;
   always @(posedge clk) begin
      if(reset) led <= 0;
      else led <= led +1 ;
   end
                   
\TLV
   m4_define(M4_BOARD, 1)  
   m4+fpga_init()
   m4+fpga_led(*led)
\SV
   endmodule
   ```
  ### b. FPGA Board output
  
  ![ezgif com-gif-maker](https://user-images.githubusercontent.com/72123647/138243601-d4a5accf-8240-465c-b465-ba96be9e956d.gif)

  ### c. Waveform
  
  ![waveform](https://user-images.githubusercontent.com/72123647/138244115-69cccf78-d4df-405b-a4b6-437563f2ac1f.PNG)

#  

## Acknowledgment
  
  I would like to thank Mr.Kunal Ghosh, Mrs. Anagha Ghosh, Mr. Steve Hoover and Mr. Bala Dinesh for the tutorial . It helped me to learn more about the FPGA and Makerchip in a very easy and structured manner. It will be very helpful for students to work on Virtual FPGA as many cannot afford the real one. It is also useful for the simulation purpose.


## References
1. https://github.com/BalaDhinesh/Digital-Design-on-FPGA--VSDOpen21
2. https://www.makerchip.com/
