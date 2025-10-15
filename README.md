# Co-sensor-DSP
# LTspice Analog Circuit Simulations

A collection of operational amplifier (Op-Amp) based analog circuit designs simulated in LTspice. This repository contains schematics for various signal processing and filtering applications commonly used in instrumentation and measurement systems.

![LTspice](https://img.shields.io/badge/LTspice-XVII-red.svg)
![Circuit Design](https://img.shields.io/badge/Analog-Circuits-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## 📁 Circuit Collection

### 1. **Op-Amp Integrator** (`opamp.asc`)
Classic integrator circuit using operational amplifier.

**Features:**
- Input: Pulse waveform (0-1V, 50ms pulse width, 100ms period)
- Integration time constant: RC = 10ms
- Power supply: ±15V
- Output: Integrated waveform

**Components:**
- Universal Op-Amp
- R1: 1kΩ (input resistor)
- R2: 10kΩ (feedback resistor)
- C1: 1µF (integration capacitor)

**Applications:**
- Waveform generation
- Analog computing
- Signal conditioning

---

### 2. **CO Signal Processing System** (`CO signal multiple systems.asc`)
Multi-stage analog signal processing chain for Carbon Monoxide (CO) sensor signal conditioning.

**System Architecture:**

#### **Stage 1: Precision Bandpass Filter**
- Sallen-Key active bandpass configuration
- Center frequency: 16 Hz
- Input: Sine wave (2.5V DC + 1.24V AC amplitude)
- R-C network for frequency selectivity

#### **Stage 2: Precision Rectifier (Full-Wave)**
- Converts AC signal to DC
- Diode-based precision rectification
- Minimal voltage drop using op-amp feedback

#### **Stage 3: Simple Bandpass Filter**
- Secondary filtering stage
- 10kΩ resistors with 1µF capacitors
- Additional noise rejection

#### **Stage 4: AC Voltage Biasing (3 Channels)**
- OP07 precision op-amp for low offset
- Reference voltage: 3.3V
- Input resistance: 6.5kΩ
- Feedback resistance: 10kΩ
- Gain resistors: 33kΩ (Rb1, Rb2)
- Compensation capacitors: 0.19µF, 4.9µF

**Power Supply:**
- ±5V for signal conditioning stages
- 3.3V reference for biasing

**Simulation Time:** 0.5s transient analysis

**Applications:**
- Gas sensor signal conditioning
- Environmental monitoring systems
- Industrial safety equipment

---

### 3. **PM-PCB (Particulate Matter Sensor Interface)** (`PM-PCB.asc`)
Sensor interface circuit with high-voltage pulse measurement capability.

**Key Features:**

#### **Input Stage:**
- High-voltage pulse input: -10V, 10µs pulse width
- Gate pulse: 5V, 1ms width, 62.5ms period
- BSS123 N-channel MOSFET switch
- 8.25kΩ current limiting resistor

#### **Signal Conditioning:**
- Op-amp buffer with unity gain
- Zener diode protection
- 100Ω input resistor with 0.1µF bypass capacitor

#### **Filter Network:**
- Variable capacitor: C3 = 10nF ± 0.1nF (parametric sweep)
- 1kΩ/10kΩ resistor divider
- 1nF noise filtering capacitor
- 2.2µF output smoothing capacitor

**Simulation Parameters:**
- `.tran 0.5s` - 500ms simulation
- `.param x=10n` - Base capacitance value
- `.step param a list -0.1n 0 0.1n` - Parametric sweep for tolerance analysis

**Applications:**
- Particulate matter sensors (PM2.5, PM10)
- Air quality monitoring
- Environmental sensing

---

### 4. **Instrumentation Differential Amplifier** (`Instrumentation Diffrential Amplifier.asc`)
Three op-amp instrumentation amplifier for precise differential measurements.

**Architecture:**

#### **Input Stage (Dual Op-Amps):**
- Two matched op-amp buffers (U1, U2)
- High input impedance
- Common-mode rejection
- Gain set by R1, R2, R3 resistors

#### **Differential Stage (Single Op-Amp):**
- Third op-amp (U3) for differential output
- Matched resistor pairs (R4/R5, R6/R7)
- Excellent CMRR (Common Mode Rejection Ratio)

#### **Bandpass Filter (Optional):**
- Sallen-Key active filter (U4)
- 3kΩ input resistor (R8)
- 32kΩ feedback resistor (R9)
- 1µF capacitors (C1, C2) for frequency response

**Power Supply:** 5V single supply

**Advantages:**
- Very high input impedance (>1GΩ)
- High CMRR (>100dB)
- Low output impedance
- Adjustable gain

**Applications:**
- Sensor signal amplification
- Biomedical instrumentation (ECG, EMG)
- Strain gauge measurements
- Thermocouple amplifiers
- Bridge circuit measurements

---

### 5. **Integrator Circuit** (`Integrator.asc`)
Standard op-amp integrator with pulse input.

**Specifications:**
- Same as "Op-Amp Integrator" above
- Input pulse: 0-1V, 50ms width
- Integration constant: R×C = 10ms
- Power: ±15V dual supply

**Transfer Function:**
```
Vout = -(1/RC) ∫ Vin dt
```

**Applications:**
- Ramp generation
- Triangular waveform synthesis
- Analog computation
- Phase shifting

---

## 🛠️ Software Requirements

### LTspice Installation
- **Download:** [LTspice XVII](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)
- **Platforms:** Windows, macOS, Linux (Wine)
- **Size:** ~80MB
- **Cost:** Free

---

## 📖 How to Use

### Opening Circuit Files

1. **Install LTspice XVII**
2. **Clone this repository**
   ```bash
   git clone https://github.com/yourusername/ltspice-circuits.git
   cd ltspice-circuits
   ```

3. **Open circuit files**
   - Launch LTspice
   - File → Open → Select `.asc` file
   - Circuit schematic will appear

### Running Simulations

1. **Start simulation:** Press `F5` or click "Run" button
2. **View results:** Waveform viewer opens automatically
3. **Add probes:** Click on circuit nodes/wires to view voltages
4. **Analyze current:** Hold `Alt` and click on component

### Modifying Parameters

**Change component values:**
- Right-click on component
- Modify value field
- Press Enter

**Edit simulation commands:**
- Right-click on `.tran` or other SPICE directives
- Modify parameters
- OK to apply

---

## 🔧 Component Reference

### Common Op-Amps Used

| Model | Type | Description |
|-------|------|-------------|
| UniversalOpAmp | Generic | Ideal op-amp for basic circuits |
| UniversalOpAmp2 | Generic | Dual supply version |
| OP07 | Precision | Low offset, low drift (<0.5µV) |

### Standard Component Values

**Resistors:**
- 100Ω, 1kΩ, 3kΩ, 10kΩ, 32kΩ
- Tolerance: ±1% (specified)
- Power: 100mW (PM-PCB circuit)

**Capacitors:**
- 1nF, 0.1µF, 0.19µF, 1µF, 2.2µF, 4.9µF
- Type: Ceramic, Film, Electrolytic

**Semiconductors:**
- BSS123: N-Channel MOSFET
- Zener diodes for protection
- Standard rectifier diodes

---

## 📊 Simulation Commands

### Transient Analysis
```spice
.tran 0 10s 0        ; Simulate 0 to 10 seconds
.tran 0 0.5s 0       ; Simulate 0 to 0.5 seconds
```

### Parametric Sweep
```spice
.param x=10n         ; Define parameter
.step param a list -0.1n 0 0.1n  ; Sweep parameter
```

### Common Voltage Sources
```spice
V=5                  ; DC voltage
PULSE(0 1 0 0 0 50m 100m)  ; Pulse: Vlow Vhigh Tdelay Trise Tfall Ton Tperiod
SINE(2.5 1.24 16 0)  ; Sine: Voffset Vamplitude Freq Phase
```

---

## 🎯 Learning Objectives

This collection demonstrates:

✅ **Op-Amp Fundamentals**
- Inverting/non-inverting configurations
- Virtual ground concept
- Feedback theory

✅ **Active Filters**
- Bandpass filter design
- Sallen-Key topology
- Frequency response analysis

✅ **Signal Conditioning**
- Amplification
- Rectification
- Biasing techniques

✅ **Instrumentation Design**
- Differential measurements
- High CMRR design
- Noise reduction

✅ **Integration Circuits**
- RC time constants
- Waveform generation
- Analog computation

---

## 📈 Expected Outputs

### Op-Amp Integrator
- Input: Square pulses
- Output: Triangular ramps (negative slope)
- Integration slope: -V/RC

### CO Signal System
- Filtered sine wave at 16 Hz
- Rectified DC output
- Biased voltage centered at 3.3V

### PM-PCB
- Pulse response with capacitive filtering
- Parametric analysis showing tolerance effects

### Instrumentation Amplifier
- Differential gain with common-mode rejection
- Optional bandpass filtering at output

---

## 🔍 Troubleshooting

### Simulation Won't Start
- Check SPICE directive syntax
- Verify all ground connections
- Ensure power supplies are connected

### Incorrect Results
- Check component values (k=kilo, µ=micro)
- Verify op-amp power supply pins
- Confirm simulation time is adequate

### No Output Signal
- Verify input source is configured
- Check probe placement
- Ensure circuit has DC path to ground

### Convergence Issues
- Add `.options plotwinsize=0` for large simulations
- Reduce simulation accuracy if needed
- Check for floating nodes

---

## 🚀 Future Enhancements

Potential additions to this collection:

- [ ] Active notch filters (50/60 Hz rejection)
- [ ] Phase-locked loops (PLL)
- [ ] Sample-and-hold circuits
- [ ] Multi-stage filter designs
- [ ] Voltage-controlled oscillators (VCO)
- [ ] Comparator and window detector circuits
- [ ] Active rectifier improvements
- [ ] Temperature compensation circuits
- [ ] PCB layout files for practical implementation

---

## 📚 Additional Resources

### LTspice Tutorials
- [LTspice Getting Started Guide](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html)
- [Op-Amp Theory](https://www.analog.com/en/design-center/landing-pages/001/amplifier-applications-guide.html)
- [Active Filter Design](https://www.ti.com/lit/an/sloa049b/sloa049b.pdf)

### SPICE Command Reference
- [SPICE Quick Reference](http://www.seas.upenn.edu/~jan/spice/spice.overview.html)
- [LTspice Help Files](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html#help-and-support)

### Circuit Design Books
- "Op Amps for Everyone" - Texas Instruments
- "The Art of Electronics" - Horowitz & Hill
- "Analog Circuit Design" - Bob Dobkin & Jim Williams

---

## 🤝 Contributing

Contributions are welcome! Ideas for new circuits:

- Voltage references
- Precision current sources
- Audio amplifiers
- ADC interface circuits
- Signal generators
- Power supply circuits

---

## 📄 License

This project is licensed under the MIT License - free to use, modify, and distribute for educational and commercial purposes.

---

## 👤 Author

**Amey**
- LinkedIn: [linkedin.com/in/amey1way](https://www.linkedin.com/in/amey1way/)

---

## 🙏 Acknowledgments

- Analog Devices for LTspice simulator
- Op-amp manufacturers for datasheets
- Electronics community for circuit designs
- Open-source hardware movement

---

## 📞 Support

For questions or circuit discussions:
- Open an issue on GitHub
- Contact via LinkedIn
- Share simulation results!

---

**Last Updated:** October 2025

💡 **Tip:** Start with the simple integrator circuit to learn LTspice basics, then progress to more complex signal processing chains!
