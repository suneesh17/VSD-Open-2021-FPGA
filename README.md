# VSD-Open-2021-FPGA-Tutorial

![137896513-0cc9dace-0454-43a7-be28-a6ce883cf631](https://user-images.githubusercontent.com/72123647/138161674-73cbdebe-5568-4381-9a06-f23f427a780f.png)

This repository contains the documentation of the tutorial on "Digital Design on FPGA", an online workshop conducted by VLSI System Design (VSD)

## Table of Contents
- [Introduction](#introduction)
- [Interfacing LEDs](#interfacing-leds)
- [LED Counter](#led-counter)
- [Interfacing LED lab](#interfacing-led-lab)
- [Seven Segment Display](#seven-segment-display)
- [4-way Traffic Light Controller](#4-way-traffic-light-controller)
- [Acknowledgement](#acknowledgement)
- [References](#references)


  
## Introduction

### 1. FPGA

 Field Programmable Gate Array (FPGA) are ICs that allows the hardware designer to program the device to perform an operation for a specific application. The term Field Programmable itself means that the IC is not fixed at the time of manufacturing but rather user defined. It is mainly used as a prototype for ASICs.
 
### 2. Verilog
  
  Verilog, a Hardware Description Language (HDL), used for describing a digital system in a more robust and flexible way. This is achieved when it creates a level of abstraction to hide away the implementation details.
  
### 3. Makerchip

  A free web based IDE for developing  high quality integrated circuits. It allows us to code, compile, simulate and debug verilog designs, all from your browser. Makerchip is also available as an app on all OS platforms.
  For more information, visit: https://www.makerchip.com/

# Interfacing LEDs
  In this section, we deal with simulation of how LEDs work by assigning random values using System Verilog.
  
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
  
  ### c. Diagram
  
  ![diagram](https://user-images.githubusercontent.com/72123647/138255356-d1d80b0e-35a9-4530-8664-25bc2a2dd523.PNG)

  ### d. Waveform
  
  ![waveform](https://user-images.githubusercontent.com/72123647/138244115-69cccf78-d4df-405b-a4b6-437563f2ac1f.PNG)

#  Interfacing LED Lab

In this section, we try to see how shift operation works by using **>>** (for right shift) and **<<** (for left shift) using System Verilog.

Refer to the link for the project: https://makerchip.com/sandbox/0VOflhxZZ/0LghYNY#
	
### a. Code
```
	\m4_TLV_version 1d: tl-x.org
	\SV
	m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
   // AUTHOR- SUNEESH HARAN
   wire [7:0] led;
	wire [7:0] led1;
	assign led= 8'b11111111;
	assign led1= led>>1;
	//assign led1= led>>4;                   
                     
	\TLV
   m4_define(M4_BOARD, 1)  
   m4+fpga_init()
   m4+fpga_led(*led1)
	\SV
   endmodule
 ```

### b. FPGA Board Output

![snap1](https://user-images.githubusercontent.com/72123647/138331740-0d9318ec-f9e7-4fa3-a85d-64c6657a2310.png)

![snap2](https://user-images.githubusercontent.com/72123647/138331747-78d6021d-e628-4bbd-9d30-7344cb7ae293.PNG)



# Seven Segment Display

In this section, we talk about displaying numbers into 7 segment display. It takes the n-bit input and generates the corresponding pattern by lighting up the appropriate LED segments in the display

![snap1](https://user-images.githubusercontent.com/72123647/138332423-37914465-10ab-4eb2-ab95-901c00b006f4.PNG)

	
### Interfacing Seven Segment

Refer to the following link for project: https://makerchip.com/sandbox/0VOflhxZZ/0X6hMB7

#### a. Code
```
	\m4_TLV_version 1d: tl-x.org
	\SV
	m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
   //AUTHOR- SUNEESH HARAN
   reg [3:0] digit;
	reg [7:0] seg;
	wire dp;
	assign dp=0;
	/*assign digit= 4'b0000;
	assign seg = 7'b0010010;*/
	assign digit = 4'b0101;
	assign seg= 7'b0100000;                 
                   
	\TLV
   m4_define(M4_BOARD, 2)  
   m4+fpga_init()
   m4+fpga_sseg(*digit,*seg,*dp)
	\SV
   endmodule
```

#### b. FPGA Board output

![snap1](https://user-images.githubusercontent.com/72123647/138365314-af08247f-253c-4903-8484-da5ced1dcdd5.png)

![snap2](https://user-images.githubusercontent.com/72123647/138365317-2242d468-6980-4a49-a0ed-6c295502a4ee.PNG)


### Interfacing Seven Segment Lab

Refer to the following link for project: https://makerchip.com/sandbox/0VOflhxZZ/0Wnhyzv#

#### a. Code

```
	\m4_TLV_version 1d: tl-x.org
	\SV
	m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
   //AUTHOR- SUNEESH HARAN
   reg [3:0] digit;
	reg [7:0] seg;
	reg [4:0] count;                   
	wire dp;
	assign dp=1;   
	always@(posedge clk)
      begin
         if(reset)
            count<=0;
         else if(count>15)
            count<=0;
         else
            count<=count+1;
            case(count)
               0: seg = 7'b0000001;
               1: seg = 7'b1001111;
               2: seg = 7'b0010010;
               3: seg = 7'b0000110;
               4: seg = 7'b1001100;
               5: seg = 7'b0100100;
               6: seg = 7'b0100000; 
               7: seg = 7'b0001111; 
               8: seg = 7'b0000000;
               9: seg = 7'b0000100; 
               10:seg = 7'b0001000;
               11:seg = 7'b1100000;
               12:seg = 7'b0110001;
               13:seg = 7'b1000010;
               14:seg = 7'b0110000;
               15:seg = 7'b0111000;
               default: seg = 7'b1111111;
              endcase
         end
                   
	\TLV
   m4_define(M4_BOARD, 2)  
   m4+fpga_init()
   m4+fpga_sseg(*digit,*seg,*dp)
	\SV
   endmodule
```
#### b. FPGA Board output

![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/72123647/138363625-f6538a77-89e7-48ec-9093-193c96181f84.gif)

# 4 Way Traffic Light Controller

In this section, we design a 4 way traffic system using Finite State Machines (FSM). The problem statement is given below

![snap1](https://user-images.githubusercontent.com/72123647/138368664-431c14b6-bd61-4a6a-89c0-c73739496269.PNG)

![flowchart](https://user-images.githubusercontent.com/72123647/138369275-010c6177-d1ec-4f07-b0c0-1d58249a3817.png)

Refer to the following link for project: https://makerchip.com/sandbox/0VOflhxZZ/0Y6h6k0

### a. Code
```
	\m4_TLV_version 1d -p verilog --bestsv --noline: tl-x.org
\SV
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/Virtual-FPGA-Lab/main/tlv_lib/fpga_includes.tlv'])                   
\SV
	//AUTHOR- SUNEESH HARAN                   
   m4_makerchip_module   
   wire [15:0] led;
   reg [3:0] digit;
   reg [6:0] segment;
   wire  dp = 1;
 
   reg [2:0] state;
   reg [2:0] count;
 
   parameter [2:0] NORTH	=	3'b000;
   parameter [2:0] NORTH_Y	=	3'b001;
   parameter [2:0] SOUTH	=	3'b010;
   parameter [2:0] SOUTH_Y	=	3'b011;
   parameter [2:0] EAST		=	3'b100;
   parameter [2:0] EAST_Y	=	3'b101;
   parameter [2:0] WEST		=	3'b110;
   parameter [2:0] WEST_Y	=	3'b111;

   always @(posedge clk, posedge reset)
     begin
        if (reset)
            begin
               
                /* TODO: Set initial state to NORTH and count signal to zero */
                 assign state= NORTH;
                 assign count = 3'b000;
               
            end
        else
            begin
                case (state)
                NORTH :
                    begin
                       
                       // Enable first seven segment and set to Green 
                       digit <= 4'b0111;
                       segment <= 7'b1110111;
                       
                        /* TODO: 1. Keep the green NORTH signal active for 8 seconds 
                                2. Set state of signal to yellow NORTH after that 
                          HINT: Use if-else block
                        */
                       if(count==7)
                          begin
                            assign state= NORTH_Y;
                             assign count=0;
                          end
                       else
                          assign count=count+1;                       
                    end

                NORTH_Y :
                    begin
                       
                        // Enable first seven segment and set to Yellow
                        digit <= 4'b0111;
                        segment <= 7'b1111110;
                       
                        /* TODO: 1. Keep the yellow NORTH signal active for 4 seconds 
                                2. Set state of signal to green SOUTH after that 
                        */
                       if(count==3)
                          begin
                             assign state=SOUTH;
                             assign count=0;
                       		end
                       else
                         assign count=count+1;
                    end

               SOUTH :
                    begin
                       
                        // TODO: Enable second seven segment and set to Green 
                       digit<= 4'b1011;
                       segment<= 7'b1110111;
                        /* TODO: 1. Keep the green SOUTH signal active for 8 seconds 
                                 2. Set state of signal to yellow SOUTH after that 
                        */
                    if(count==7)
                          begin
                             assign state= SOUTH_Y;
                             assign count=0;
                          end
                       else
                          assign count=count+1; 
                       
                    end

                SOUTH_Y :
                    begin
                    
                        // TODO: Enable second seven segment and set to Yellow 
                    		digit<= 4'b1011;
                      	segment<= 7'b1111110;
                        /* TODO: 1. Keep the yellow SOUTH signal active for 4 seconds 
                                    2. Set state of signal to green EAST after that 
                        */
                    		if(count==3)
                          begin
                             assign state=EAST;
                             assign count=0;
                       		end
                       else
                          assign count=count+1;
                    end
                   
                EAST :
                    begin
                    
                        // TODO: Enable third seven segment and set to Green 
                    digit<= 4'b1101;
                     segment<= 7'b1110111;
                        /* TODO: 1. Keep the green EAST signal active for 8 seconds 
                                2. Set state of signal to yellow EAST after that 
                        */
                    if(count==7)
                          begin
                             assign state= EAST_Y;
                             assign count=0;
                          end
                       else
                          assign count=count+1; 
                    end
                EAST_Y :
                    begin
                    
                    // TODO: Enable third seven segment and set to Yellow 
                     digit<= 4'b1101;
                        segment<= 7'b1111110;
                    /* TODO: 1. Keep the yellow EAST signal active for 4 seconds 
                                2. Set state of signal to green WEST after that 
                    */
                   if(count==3)
                          begin
                            assign state=WEST;
                             assign count=0;
                       		end
                       else
                         assign count=count+1;
                    end
                WEST :
                    begin

                    // TODO: Enable fourth seven segment and set to Green 
							digit<= 4'b1110;
                   segment<= 7'b1110111;
                    /* TODO: 1. Keep the green WEST signal active for 8 seconds 
                            2. Set state of signal to yellow WEST after that 
                    */
							if(count==7)
                          begin
                            assign state= WEST_Y;
                            assign count=0;
                           end
                       else
                         assign count=count+1;
                    end
                WEST_Y :
                    begin

                    // TODO: Enable fourth seven segment and set to Yellow 
							digit <= 4'b1110;
                     segment <= 7'b1111110;
                    /* TODO: 1. Keep the yellow EAST signal active for 4 seconds 
                            2. Move back to NORTH signal again
                    */
							if(count==3)
                          begin
                            assign state=NORTH;
                            assign count=0;
                       		end
                       else
                          assign count=count+1;
                    end
            endcase 
        end 
    end 
	assign led = count;

\TLV
   // M4_BOARD numbering
   // 1 - Zedboard
   // 2 - Artix-7
   // 3 - Basys3
   // 4 - Icebreaker
   // 5 - Nexys
   m4_define(M4_BOARD, 3)
   m4+fpga_init()
   m4+fpga_led(*led)
   m4+fpga_sseg(*digit, *segment, *dp)
\SV
   endmodule
```

### b. FPGA Board output

![ezgif com-gif-maker (2)](https://user-images.githubusercontent.com/72123647/138369230-5db10e34-a930-4e64-a312-2bf0f3726fcf.gif)


## Acknowledgement
  
  I would like to thank Mr.Kunal Ghosh, Mrs. Anagha Ghosh, Mr. Steve Hoover and Mr. Bala Dinesh for the tutorial . One can learn more about FPGAs and its implementation in real life scenarios. Since actual FPGA boards are expensive and cannot be afforded by everyone, the Makerchip platform plays a vital role where it provides a platform to run the codes on virtual FPGA boards.

## References
1. https://github.com/BalaDhinesh/Digital-Design-on-FPGA--VSDOpen21
2. https://www.makerchip.com/
