# G27-based OpenFFB Build

The goal of this article is to document @willson556's G27-based build. The hope is to provide detailed information, including pricing, on a cheap and relatively cost effective race-ready OpenFFB setup.

It's expected that the build outlined here will also be compatible with G25 and G29 components but that still needs to be analyzed.

Total Cost if assembling driver board manually: [Placeholder]  
Total Cost with all SMT assembly done by supplier: [Placeholder]

## Table of Contents
- [G27-based OpenFFB Build](#g27-based-openffb-build)
  - [Table of Contents](#table-of-contents)
  - [Required Tools](#required-tools)
    - [Extra Tools for DIY SMT Assembly](#extra-tools-for-diy-smt-assembly)
  - [Getting and Assembling the PCBs](#getting-and-assembling-the-pcbs)
    - [Ordering boards from JLCPCB](#ordering-boards-from-jlcpcb)
    - [Ordering components from Digikey](#ordering-components-from-digikey)
    - [DIY Assembly of TMC4671 Driver Board](#diy-assembly-of-tmc4671-driver-board)
    - [Ordering TMC4671 Driver Board Assembles from PCBWay (or PCBFabExpress?)](#ordering-tmc4671-driver-board-assembles-from-pcbway-or-pcbfabexpress)
  - [Motor and Mount](#motor-and-mount)
  - [Power Supply](#power-supply)
  - [System Assembly](#system-assembly)
  - [First Power On](#first-power-on)
  - [Configuration](#configuration)

## Required Tools

- Wire Strippers
- Phillips #2 Screwdriver
- Phillips #1 Screwdriver
- Soldering Iron with Fine Tip (ex: Weller WE1010NA w/ ETP tip)
- Fine Solder (ex: 63/37 0.38mm diameter with no-clean flux core)
- Crimper for 0.1" Housing Pins (ex: [Crimping Tool: 0.1-1.0 mm² Capacity, 16-28 AWG](https://www.pololu.com/product/1928))
- 3D Printer for G27 Wheel Mount
- Basic Wrench Set
- Basic Allen Wrench Set
- Drill w/ Drill Bits
- Hammer
- Wood Saw

### Extra Tools for DIY SMT Assembly

- Solder Paste (ex: MG Chemicals 4860P 63/37 No Clean)
- Fine solder paste tip (ex: <https://www.mcmaster.com/6710A74/>)
- Recommended: Sturdy Syringe Plunger (ex: <https://www.mcmaster.com/66045A13/>)
- Solder Wick (ex: [NTE Electronics SW02-10 No Clean Solder Wick](https://www.amazon.com/NTE-Electronics-SW02-10-No-Clean-Blue-098/dp/B0195UVWJ8/ref=pd_bxgy_2/147-0225496-6412450?_encoding=UTF8&pd_rd_i=B0195UVWJ8&pd_rd_r=62e358ce-22b7-4e2a-a3cd-7f90774c0fe1&pd_rd_w=ZzOtA&pd_rd_wg=GujPr&pf_rd_p=f325d01c-4658-4593-be83-3e12ca663f0e&pf_rd_r=S8VD1BZ1ARVD36R1JNZ7&psc=1&refRID=S8VD1BZ1ARVD36R1JNZ7))
- Hot Air SMD Rework Station (ex: <https://www.amazon.com/gp/product/B07Y337XPT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1>)
- Flux (ex: [No Clean Tacky Soldering Flux 5 Grams](https://www.amazon.com/gp/product/B07DCD9M3P/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1>))

## Getting and Assembling the PCBs

This build revolves around 3 PCBs:

- **OpenFFBoard-main**: This board contains an STM32F407VG microcontroller. It is responsible for interfacing with the USB port, shifters/buttons/pedals, and the motor driver (TMC4671 based stepper/PMSM/BLDC driver or other driver through PWM).
- **TMC4671-driver**: This board contains the TMC4671-LA motor control IC that is capable of running stepper and BLDC/PMSM/PMAC motors. It is capable of running up to 48VDC on the input and 20A motor phase current.
- **G27InterfaceBoard**: This board contains hardware to interface the G27 pedals, shifter, and wheel buttons with the **OpenFFBoard-main**. It has two DB9 connectors to plug in the pedals and shifter (no custom harness required) and an RJ45 (Ethernet) for the wheel buttons (you'll need to build a harness for this).

The **OpenFFBoard-main** and **G27InterfaceBoard** can both be ordered mostly assembled from JLCPCB -- only easy to solder through-hole components have to be done manually. The **TMC4671-driver** on the other hand cannot. You have two main options here: order it from another supplier or attempt to assemble it yourself.

### Ordering boards from JLCPCB

[Placeholder]

### Ordering components from Digikey

The components for the main board and G27 interface board that JLCPCB won't populate as well as all the components for the TMC4671 driver board are in [G27-Build-BOM](G27-Build-BOM.ods) on the Digikey page. You should be able to save the "Digikey" sheet as a CSV and import directly into Digikey's website.

[Placeholder]

### DIY Assembly of TMC4671 Driver Board

[Placeholder]

### Ordering TMC4671 Driver Board Assembles from PCBWay (or PCBFabExpress?)

[Placeholder]

## Motor and Mount

The ideal motor for OpenFFB is the Mige 130ST-M10010. It has plenty of torque (even if you upgrade to a larger wheel rim in the future) and is relatively efficient in this operating range. There are other options available, see [Open FFBoard update 1: Servos and GUIs](https://www.youtube.com/watch?v=gG_dbnKfH5Q) for some comparisons.

Mige motors can be ordered directly from [Mige on Alibaba](https://www.alibaba.com/product-detail/small-Mige-130ST-M10010-ac-servo_60393398363.html?spm=a2700.7724857.normal_offer.d_title.8c03166fz2C3Sr).

Pricing at the time I ordered (Dec 2020) was:
| Item                                        | Price    |
| ------------------------------------------- | -------- |
| 130ST-M10010 w/ 10K PPR Encoder & 3M Cables | $172 USD |
| Shipping to San Jose, CA                    | $139 USD |
| **Total**                                   | $311 USD |

As you can see, shipping is a substantial portion of the cost. There was no import duty coming into the USA.

For the mounting bracket, I used a simple [right-angle bracket from AliExpress](https://www.aliexpress.com/item/4001079488981.html?spm=a2g0s.9042311.0.0.4bca4c4dr02dnM). This was $43.47 USD delivered to San Jose, CA.

## Power Supply

You need a power supply that outputs between 36V and 48V and is capable of supplying between 5A and 10A. I acquired a used [Mean Well HRPG-450-48](https://www.ebay.com/itm/Mean-Well-HRPG-450-48-AC-DC-Power-Supply-Single-OUT-48V-9-5A-CNC-Router-Servo/183410848369?epid=662180952&hash=item2ab4237271:g:9tAAAOSw4M9bitsA) for $52.84 USD delivered (about 1/3 of a new one).

## System Assembly

[Placeholder]

## First Power On

[Placeholder]

## Configuration

[Placeholder]