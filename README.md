# 📖 Silicon Saga — Chapter 2  (Week 2)
## Task 1: Understanding SoC Fundamentals & BabySoC Functional Modelling  

**Aim:** Building a strong foundation in SoC design by exploring the fundamentals and practicing functional modelling using **Icarus Verilog** & **GTKWave**.  

---

## 🎯 Objective
To build a solid understanding of **System-on-Chip (SoC) fundamentals** and practice functional modelling of the **BabySoC** using simulation tools.  

---

## 🗂️ Focus Areas (TASK-1)

- [🔹 What is a System-on-Chip (SoC)?](#-what-is-a-system-on-chip-soc)  
- [🔹 Components of a Typical SoC](#-components-of-a-typical-soc)  
- [🔹 Why BabySoC?](#-why-babysoc)  
- [🔹 Role of Functional Modelling](#-role-of-functional-modelling)  

---

## 🔹 What is a System-on-Chip (SoC)?
A **System-on-Chip (SoC)** is an integrated circuit that integrates multiple essential system components into a single silicon chip.  
Instead of having separate chips for CPU, memory, and peripherals, SoC unifies them, improving **performance, efficiency, and size optimization**.  

## 🔹 Why SoCs Are Awesome (Advantages)

| **Advantage** | **Description** |
|---------------|------------------|
| **Energy Efficiency** | Components are closely packed, reducing data travel distance and minimizing power loss. Crucial for battery-operated devices. |
| **Space Saving** | Consolidating multiple chips into one drastically reduces the overall footprint. Enables smaller, more portable devices. |
| **High Performance** | Faster communication between internal components (low latency) results in quicker data processing. |
| **Cost Effective** | Manufacturing a single, highly integrated chip is generally cheaper than manufacturing and assembling many separate components. |
| **Reliability** | Fewer physical interconnects and solder points mean fewer potential points of failure. |

---

---

## 🔹 Components of a Typical SoC

| **Component** | **Function** | **Role in Device Performance** |
|---------------|--------------|--------------------------------|
| **CPU (Central Processing Unit)** | The "brain"; handles main instructions, calculations, data processing, and application management. | Executes general-purpose tasks and dictates overall processing speed. |
| **GPU (Graphics Processing Unit)** | Show visuals, manages graphics processing for display, gaming, and animations. | Critical for a smooth user interface, high-resolution video, and gaming performance. |
| **DSP (Digital Signal Processor)** | Specialized for processing audio, video, and other continuous signals. | Enables features like noise reduction, voice recognition, and real-time media encoding/decoding. |
| **Memory (RAM, ROM/Flash)** | RAM stores temporary data for running applications; ROM/Flash stores permanent system and user data. | Determines the device's multitasking capability and overall storage capacity. |
| **I/O Ports (Input/Output)** | Connects the chip to external devices like cameras, sensors, USB, and audio devices. | Allows the SoC to send and receive data from the outside world. |
| **Power Management Unit (PMU)** | Regulates voltage and current, managing power distribution across all blocks. | Essential for optimizing energy efficiency and extending battery life. |
| **Special Features** | Includes connectivity modules (Wi-Fi, Bluetooth, GPS), security engines, and hardware accelerators. | Provides wireless communication and enhances security and specific task speed (e.g., AI processing). |


---

Together, these form a **complete computing system on a single chip**. 

---

## 🔹 Soc Design Flow...

![designflow](/assets/vsd%20soc%20flow.png)

---

## 🔹 Why BabySoC?
**BabySoC** is a simplified teaching model of an SoC.  
- Strips down complexity while retaining core concepts.  
- Helps beginners visualize how CPU, memory, and peripherals work together.  
- Provides a sandbox for learning **functional modelling** before diving into full-scale RTL design and physical implementation.  
- Ensures **step-by-step learning** without being overwhelmed by industrial-level SoC designs.  

 **The VSDBabySoC** is a small, specialized System on Chip (SoC) designed primarily as a testing ground for new components. 

 ## The main goal is two-fold:
-*First-Time Testing:* To integrate and test three specific, open-source hardware blocks (the RVMYTH, PLL, and DAC) together for the first time.
-*Analog Calibration:* To accurately tune its analog components (like the PLL and DAC) for reliable real-world use.

## ⚙️ How the VSDBabySoC Works (The Process Flow) 
The chip follows a three-step cycle to generate an output signal:

*1. Initialization and Synchronization (The Clock)*
When the SoC turns on, the 8x PLL immediately activates.
Result: The PLL generates a precise, stable, and synchronized clock signal. This signal acts like a conductor , ensuring the RVMYTH and DAC operate at the exact same pace, preventing any timing errors or data corruption.

*2. Data Processing (The Digital Signal)*
The RVMYTH processor starts executing instructions.
Mechanism: It uses a dedicated area called the r17 register to hold and repeatedly update a sequence of digital values. This creates a continuous stream of digital data.

*3.  Analog Signal Generation (The Output)*
 The 10-bit DAC receives the constantly changing digital values from the RVMYTH's r17 register.
Result: The DAC translates these digital numbers into a physical, continuous analog electrical signal. This output, saved to a file named OUT, can then be used to drive external consumer devices (like older TVs or mobile audio ports) to produce sound or video.

---

### 📊 BabySoC Components Breakdown  

| **Component** | **What It Is**              | **Its Job on the Chip** |
|---------------|------------------------------|--------------------------|
| **RVMYTH**    | A Microprocessor Core        |  It handles all the data processing and calculations, and cycles through the digital values to be converted. |
| **8x PLL**    | Phase-Locked Loop            |  It takes the initial input signal and generates a super-stable, synchronized clock signal for the entire system. |
| **10-bit DAC**| Digital-to-Analog Converter  | It takes the digital numbers from the RVMYTH and converts them into a continuous, usable analog signal. |


---

## 🔄 Phase-Locked Loop (PLL): The On-Chip Clock Synchronizer
A Phase-Locked Loop (PLL) is an essential control system that generates an output signal perfectly synchronized in phase and frequency with an input signal. It acts as an on-chip timing lock for the entire system.

*Phase-Locked Loop (PLL) Components and Key Mechanisms*

| **Component** / **Key Mechanism** | **Function** / **Details** |
|---------------------------|-----------------|
| **Phase Detector (PD)** | Compares the phase of the input (reference) signal with the PLL's output signal and generates an error voltage proportional to the difference. |
| **Loop Filter (LF)** | A low-pass filter that smooths the error voltage, filtering out noise and high-frequency components to produce a stable control voltage. |
| **Voltage-Controlled Oscillator (VCO)** | Generates the output signal, adjusting its frequency based on the control voltage from the Loop Filter. |
| **Core Goal** | To "lock" the output frequency to the input frequency, maintaining a constant (often zero) phase relationship. |
| **Frequency Multiplication** | By adding a frequency divider in the feedback path, the PLL can generate an output frequency that is an exact multiple of the input frequency. |

---

## Why On-Chip Clocks Are Important

1. **Timing & Distribution**
   - Long wiring on large chips causes delays; different parts may get the clock at slightly different times.
   - Off-chip clocks can suffer from **jitter**, reducing timing precision.

2. **Frequency Flexibility**
   - Chips often need multiple frequencies (e.g., CPU vs peripheral). PLLs can generate several synchronized clocks from one reference.

3. **Accuracy & Stability**
   - Quartz crystals have small frequency errors (ppm) that increase over time due to temperature changes and aging.
   - PLLs adjust continuously to maintain a precise and stable internal clock.

   ---
# 🎛️ Digital-to-Analog Converter (DAC): The Digital Translator

A **Digital-to-Analog Converter (DAC)** converts a digital input (0s and 1s) into a real-world analog signal (continuous voltage or current), allowing digital devices to interact with the physical world.

## Structure & Representation

| *Aspect* | *Description* |
|--------|------------|
| Digital Input | A series of binary bits. The number of bits (resolution) determines how many distinct analog levels the DAC can produce. |
| Physical Structure | Multiple binary inputs and a single continuous analog output. The number of inputs is usually a power of two (2, 4, 8, 16, etc.). |

## Common Types of DACs

| *Type* | *Description* |
|------|------------|
| Weighted Resistor DAC | Uses resistors with specific weights corresponding to each input bit (e.g., R, R/2, R/4…). |
| R-2R Ladder DAC | Uses a repeating network of only two resistor values (R and 2R). Simple to manufacture and scalable for higher resolutions. |

## DAC in VSDBabySoC

In the **VSDBabySoC**, the **10-bit DAC** converts digital data from the **RVMYTH processor** into a smooth analog voltage. This allows devices like TVs or mobile phones to produce sound or video from digital signals.


## 🔹 Role of Functional Modelling
Before RTL design and physical implementation, **functional modelling** plays a critical role:  
- Allows early testing of **logic flow & interactions** between components.  
- Helps in validating the **architecture & specifications**.  
- Saves time and cost by identifying design issues before RTL synthesis.  
- Simulation tools like **Icarus Verilog** and **GTKWave** help visualize signals and ensure correctness at this conceptual stage.  

---

## 📝 Reflection
This task strengthened the foundation of **SoC thinking**  understanding not just the CPU, but the **entire system** as a unified design.  
By practicing **functional modelling with BabySoC**, we take the first step toward the **bigger picture** of RTL and physical design flow.  

---

## Task 2:– Labs (Hands-on Functional Modelling) 

# 🔗 Cloning the Project
To begin, clone the VSDBabySoC repository using the following command:

*git clone https://github.com/manili/VSDBabySoC.git*
 

![gitclone](./assets/git%20clone.png)

---

To check if the command get cloned or not :

![gitclone2](./assets/git%20clone%202.png)

---

# TLV to Verilog Conversion for RVMYTH
Initially, you will see only the rvmyth.tlv file inside src/module/, since the RVMYTH core is written in TL-Verilog.
To convert it into a .v file for simulation, follow the steps below:
*🔧 TLV to Verilog Conversion Steps*

```
# Step 1: Install python3-venv (if not already installed)
sudo apt update
sudo apt install python3-venv python3-pip

# Step 2: Create and activate a virtual environment
cd VSDBabySoC/
python3 -m venv sp_env
source sp_env/bin/activate

# Step 3: Install SandPiper-SaaS inside the virtual environment
pip install pyyaml click sandpiper-saas

# Step 4: Convert rvmyth.tlv to Verilog
sandpiper-saas -i ./src/module/*.tlv -o rvmyth.v --bestsv --noline -p verilog --outdir ./src/module/
```

# VSDBabySoC RTL to Gate-Level Simulation Flow

# 1️⃣ Pre-Synthesis Simulation:
   - Compile RTL with Icarus Verilog
   - Purpose: Verify RTL functionality before synthesis
   - Output: output/pre_synth_sim/pre_synth_sim.out and waveform .vcd
 
Run the following command to perform a pre-synthesis simulation:
```
iverilog -o output/pre_synth_sim/pre_synth_sim.out   -DPRE_SYNTH_SIM   -I src/include   -I src/module   src/module/testbench.v
```
![presynth](./assets/pre_synth%20terminal.png)

*Follow these commands in vsdbabysoc directory to see output in gtk wave*
 ```
 pre_synth_sim/
 ls
post_synth_sim.out  pre_synth_sim.out

```
![output](./assets/pre_synth%201.png)
![output](./assets/pre_synth%202.png)

- The continuous, sine-like wave (labeled OUT) confirms that the Digital-to-Analog Converter (DAC) module is working correctly in the ideal, functional simulation. 
- The digital bus RV_TO_DAC[9:0] is showing changing values (e.g., 334 or 231 in other views). This proves that the RVMYTH processor core is actively generating and sending data to the DAC.

 **The pre-synthesis waveform verifies the logical correctness (functionality) of  design without worrying about the physical delays**
 
 ---
# 2️⃣ Post-Synthesis Simulation:
 
 - Compile synthesized netlist + standard cells with Icarus Verilog
   - Purpose: Verify gate-level behavior matches RTL
   - Output: output/post_synth_sim/post_synth_sim.out and waveform .vcd
   Run the following command to perform a pre-synthesis simulation:

```
iverilog -o output/post_synth_sim/post_synth_sim.out -DPOST_SYNTH_SIM  -I src/include/ -I src/module/ src/module/testbench.v
```
![postsynth](./assets/post_synth%20terminal.png)

*Follow these commands in vsdbabysoc directory to see output in gtk wave*
 ```
 cd post_synth_sim/
ls
post_synth_sim.out  post_synth_sim.vcd
```
![output](./assets/post_synth%202.png)
![output2](./assets/post_synth%202.png)

- Post-Synthesis Waveform Tells Us Logical Functionality is Confirmed.
- It models the real timing delay of the physical gates.
- Verify Timing and Functionality after mapping to the PDK (Sky130).

---


## 📚 Learnings & Reflections  

This journey wasn’t just about running commands, but about **understanding the “why” behind each step**.  
Here’s what I gained:  

- 🖥️ **Linux Confidence** – Navigating the filesystem, handling errors like “No such file or directory,” and realizing the importance of correct paths.  
- 🔧 **Tool Familiarity** – From cloning repositories to installing open-source VLSI tools, I learned how these building blocks fit into a larger flow.  
- 🤔 **Problem-Solving Mindset** – Every error taught me something new; instead of frustration, I learned to approach it with curiosity.  
- 🌱 **Growth Mindset** – I saw my progress from being stuck on simple commands to confidently moving through structured flows.  

---

## ✨ Closing Note  

This repository reflects not just my technical work but also my **growth as a learner in VLSI design**.  
I started with small steps, faced hurdles, and gradually built a stronger understanding of how open-source flows are set up and run.  

I know this is only the **beginning of a longer journey**, but documenting my process here makes me appreciate every bit of progress.  
Here’s to more experiments, more mistakes, and more learning 🚀  

*— Neeharika Chauhan*  

---
 ![Author: Neeharika Chauhan](https://img.shields.io/badge/author-Neeharika%20Chauhan-blue)

 ---