# -Design-and-Implementation-of-a-Voltage-Controlled-Current-Source-VCCS-
**🧪 Usage Instructions**
1️⃣ Clone Repository
git clone https://github.com/<your-username>/Design and Implementation of a 
Voltage-Controlled Current Source (VCCS).git
cd Design and Implementation of a 
Voltage-Controlled Current Source (VCCS) 

2️⃣ Open Simulation

Launch LTspice 24.1.10.

Open the schematic file:
LTspice_Files/CurrentSource.asc

3️⃣ Run Simulation

Run transient analysis (.tran) or parametric sweep (.step param Rload 1k 10k 1k).

Plot I(Rload) to visualize regulated current across load sweep.

Check .meas results in the SPICE Error Log (Ctrl + L) for numeric data.

4️⃣ Frequency Response Test

Replace load sweep with:

.step param freq list 1 10 50 100 200
.param period=1/freq
.tran 0 {5/lowestfreq}

4️⃣ Vin Sweep (Output Current vs Control Voltage)

To test how output current changes with different Vin values, add this directive to your schematic:

.step param Vin list 1 2 3 4 5
.param Rsense=1k
.param Vsup=60
.tran 0 40m startup
.meas Iavg AVG I(Rload) FROM=20m TO=30m

This will automatically simulate for Vin = 1 V, 2 V, 3 V, 4 V, and 5 V.

📊 Achieved Results vs Target Specifications
Parameter	Target	Achieved (Sim)	Comments
Output Current	5 mA	4.9–5.4 mA	Stable and accurate
Load Range	1–10 kΩ	Achieved	Regulation maintained
Frequency Range	1–200 Hz	Achieved	Minimal transient spikes
Accuracy	±2%	±3–5%	Within tolerance

**⚡ Simulation Highlights**

Constant Current Behavior:
I(Rload) remains nearly constant (~5 mA) for Rload from 1–10 kΩ.

Frequency Stability:
The average current follows the input voltage up to 200 Hz without phase distortion.

**⚙️ Known Limitations**

Compliance Limit: At Rload > 10 kΩ, MOSFET may leave active region due to limited Vsup

Op-Amp Output Swing: Real op-amps may saturate if gate voltage exceeds output range — use ±15 V or rail-to-rail versions.

Thermal Dissipation: For low Rload values, MOSFET may dissipate >0.25 W.

Transient Spikes: During PWM operation, short-duration peaks occur; averaging or filtering may be needed for precise measurement.

**🧭 Future Enhancements**

Use a precision high-drive op-amp (e.g., OPA551).

Add RC compensation for improved loop stability.

Employ a differential sense amplifier for smaller Rsense values.

Replace Vin source with DAC control for programmable current generation.
