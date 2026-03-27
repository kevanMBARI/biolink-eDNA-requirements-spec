# BioLink "Middleware" Functional Requirements

---

## Table of Contents

- [Middleware Functional Requirements Document](#middleware-functional-requirements-document)
  - [Middleware Process Block Diagram](#middleware-process-block-diagram)
  - [Sampler](#sampler)
  - [Middleware](#middleware)
  - [Analytical Device](#analytical-device)
- [Middleware Architecture: Purpose and Function](#middleware-architecture-purpose-and-function)
- [Critical Interface Functional Requirements](#critical-interface-functional-requirements)
  - [Sampler to Middleware Interface](#sampler-to-middleware-interface)
  - [Gas and Pneumatic Chip Interface](#gas-and-pneumatic-chip-interface)
  - [Middleware Reagent Interface](#middleware-reagent-interface)
  - [Middleware and Chip Waste Management](#middleware-and-chip-waste-management)
  - [Middleware to Analytical Device Interface](#middleware-to-analytical-device-interface)
  - [Electrical (Power and Control) Interface](#electrical-power-and-control-interface)
  - [Thermal Management Interface](#thermal-management-interface)
  - [Mechanical Docking (Middleware to Chip)](#mechanical-docking-middleware-to-chip)

---

# Middleware Functional Requirements Document

## Middleware Process Block Diagram

*(Block diagram: Sampler → Middleware → Analytical Device)*

---

## Sampler

**Primary function:** Collects and processes water samples to generate a "native homogenate" that is suitable for downstream analyte detection and further modification. Transform a raw environmental sample into standardized native homogenate.

### Sampler Functional Requirements:

1. Sample Acquisition
2. Analyte Concentration
3. Sample Processing: Lysis/Homogenization
   - a. Release nucleic acids or biomolecules
   - b. Generate uniform suspension — homogenate
   - c. Homogenate has defined characteristics
4. Sample Delivery
   - a. Transfer specified volume of homogenate to middleware
   - b. Maintain sample integrity during transfer
5. Sample Preservation (Parallel Function)
6. Operational Control
   - a. Execute programmed sampling protocols
   - b. Coordinate with the middleware for sample delivery

### Sampler Key Inputs:

1. Environmental Water
2. Power
3. Reagents
4. Gas/Pressure
5. Control Signals

### Sampler Key Outputs:

1. Native/Environmental Homogenate
2. Status/Coordination Signals (handshakes)

---

## Middleware

### Primary function:

Bridge sampler output to analytical device input through lab-on-chip-based (LOC) sample modification. Processing hub to convert native homogenate to a modified product for further downstream analysis or direct analyte detection using LOC technology that conforms to a standard form factor.

### Middleware Functional Requirements:

1. Native Homogenate (Sample) Reception & Routing
2. Reagent Management
   - a. Store, manipulate and delivery
   - b. Stability
3. Lab on Chip Control
   - a. Pneumatic
   - b. Fluidic
   - c. Thermal Control
   - d. Electrical/optical sensing
4. Physical Integration
   - a. Chip positioning
   - b. Hermetic connections/sealing
   - c. Contamination prevention
5. Make/Break Connection to Sampler and Analytical Device
   - a. Accept Native Homogenate
   - b. Transfer Modified Sample to Analytical Device
6. Waste Management
7. System Coordination
   - a. Execute overall fluidic/pneumatic workflow

### Middleware Key Inputs:

1. Native Homogenate (from sampler)
2. Microfluidic Chips
3. Middleware Reagents
4. Gas/Pressure Supply
5. Power
6. Thermal Energy
7. Control Signals
8. Sampler status/coordination signals

### Middleware Key Output:

1. Modified sample (assay ready) from native homogenate
2. Status/Coordination Signal Control to Analytical Device
3. Actionable biological information (target analyte presence/absence, abundance, etc.)

### Middleware Operating Environmental Requirements

#### External Conditions the Middleware Must Operate/Tolerate:

**Temperature**

> **ENV-1.1:** The MW shall function correctly throughout an operational ambient temperature range of 4–50°C, with a target operating range of 10–17°C for typical deployments.

> **ENV-1.2:** The MW and chip shall survive exposure to non-operating temperatures of 0–35°C without permanent damage, encompassing storage and transport conditions.

- If reagent survival is not achievable under these conditions, the use of a cooling thermoelectric cooler (TEC) on the platform shall be investigated to maintain the storage environment within the allowable range of reagent stability.

**Humidity**

> **ENV-1.3:** The MW and chip shall tolerate relative humidity of 0–70% without degradation or failure during operation.

**Mechanical Environment**

> **ENV-1.4:** Platform Motion, Shock, and Vibration Tolerance (Future Platform Integration Requirement) — The MW system shall be designed to be mechanically robust and tolerant of platform-induced pitch, roll, linear acceleration, shock, and vibration environments representative of anticipated deployment platforms, including consideration of representative autonomous underwater vehicle (AUV) mechanical environments. Note: Current reference platform is the MBARI LRAUV.

- For the purposes of MW breadboard system development, these environmental requirements are considered future platform integration requirements and are out of scope for verification and compliance in the current development phase.
- Future design considerations shall account for operation under platform pitch and roll conditions within ±30° (target) to ±45° (maximum), linear acceleration loads up to ±2g, and platform vibration environments without structural damage, connector disengagement, fastener loosening, resonance, or degradation in functional performance during or after exposure. Detailed environmental specifications and verification requirements shall be defined based on the target deployment platform.

**Pressure**

> **ENV-1.5:** The MW shall function correctly at the ambient pressure condition in which it is installed, with a target equivalent to the host sampler platform operating environment and a maximum operating depth of 300 m. The MW is not necessarily required to be its own independent pressure boundary. Note: Current reference platform is the MBARI 3G ESP.

**Deployment Duration and Reagent Stability**

> **ENV-1.6:** The MW shall remain deployed and operational for a minimum of 1 week, with a target deployment duration of 2–4 weeks and a maximum of 2 months. All reagents shall remain stable, and seals shall maintain integrity for the full deployment duration.

> **ENV-1.7:** All MW reagents shall maintain activity and stability under deployment storage conditions for a target shelf-life of 2 months. Reagent stability under deployment temperatures and humidity is a critical path item requiring validation testing.

---

## Analytical Device

**Primary Function:** Convert modified sample into actionable biological information. Performs analysis of pre-prepared sample (e.g., for sequencing or other analytical device such as electrochemical or photonic array, etc.)

### Analytical Device Functional Requirements:

1. Sample Reception
2. Detection and Analysis
3. Waste management
4. Data capture and processing
5. Information output
6. Operational control
   - a. Coordination with middleware for sample input

### Analytical Device Key Inputs:

1. Modified Sample
2. Analytical Reagents
3. Power
4. Data Storage
5. Control Signals
6. Computational Resources
7. Environmental Stability

### Analytical Device Key Output:

1. Actionable biological information (species presence/absence, abundance, etc.)
2. Signal control to global system

---

# Middleware Architecture: Purpose and Function

## Primary Purpose:

The middleware is the universal adapter and orchestrator that:

1. Bridges incompatible systems — connects devices that were not designed to work together
2. Enables modularity — allows swapping different chips, samplers or analytical devices
3. Enables autonomous operations — removes human intervention between sample collection and analysis
4. Enables serial processing — processes multiple samples sequentially (e.g., 30 or some defined number consistent with operational needs) without manual intervention

## Functional Architecture:

1. **Translation Function**
   - a. Accepts native homogenate/lysate from sampler (any format) via defined interface (e.g., pierceable septa or alternative)
   - b. Accepts microfluidic chip designs via defined interface
   - c. Provides transfer of lysate to the chip over a specified volume range compatible with chip input requirements; final volumetric metering and conditioning are implemented by chip-integrated mechanisms.
   - d. Delivers modified sample in format analytical device needs via defined interface.

2. **Resource Management Function:**
   - a. Centralize common resources
     - i. Reagent storage
     - ii. Gas/pressure supply
     - iii. Thermal control (heating/cooling)
     - iv. Power distribution
     - v. Control logic
   - b. Distributes to individual chips as needed

3. **Contamination Prevention Function**
   - a. Fluidic pathways shall be single-use unless the pathway can be demonstrably cleaned or validated to prevent cross-contamination between samples.
   - b. Hermetic sealing
   - c. Make/break connections
   - d. Isolated or offboard waste collection

4. **Standardization Function**
   - a. Defined standard chip interface
     - i. Port locations (standardize grid)
     - ii. Connection types and numbers (fluidic, pneumatic, electrical)
   - b. Chip agnostic design

5. **Orchestration Function**
   - a. Orchestration of three independent systems (sampler, chip, analytical device) — coordination of timing, sample transfer, workflows, etc.
   - b. Coordinate sample handoff from sampler
   - c. Executes chip processing protocols — valving sequence, thermal cycling, timing
   - d. Manages product delivery to analytical device

6. **Scalability Function**
   - a. Process up to 30 samples per deployment without human interference
   - b. Multiple sample processing architecture

---

# Critical Interface Functional Requirements

## Sampler to Middleware Interface

**Functional Purpose:** Transfer processed native homogenate from sampler to middleware with sufficient volume and integrity for downstream processing

### Functional Requirements:

**Volume Delivery**

> **IF-1.1:** The MW shall receive and retain a usable homogenate sample volume from the sampler for chip processing, with an acceptable delivered volume range of 10–500 µL and a target delivery volume of 50 µL.

> **IF-1.2:** The MW shall deliver sample volume with acceptable precision and repeatability, achieving ±5% of the target volume across 20–30 sequential samples.

**Sample Integrity**

> **IF-1.3:** The MW shall maintain DNA/RNA integrity during sample transfer such that sample composition remains unchanged from sampler output to chip input, with no degradation or dilution.

**Contamination Prevention**

> **IF-1.4:** The MW shall introduce zero external DNA/RNA during the sample transfer process. Negative controls shall remain negative with no false positives detected.

**Flow and Pressure**

> **IF-1.5:** The MW shall control sample delivery flow rate within 10–500 µL/min, with a target of 100 µL/min, to prevent bubble formation while completing transfer in a reasonable time.

> **IF-1.6:** The MW shall deliver sample at a pressure the chip can tolerate, with an operating range of 0–1000 kPa and a target delivery pressure of 350 kPa or such that it does not exceed the chip maximum allowable pressure and does not cause leakage or damage.

- The MW shall support a nominal target delivery pressure of 350 kPa and shall be designed to accommodate chip maximum allowable pressure values to be defined by chip validation testing. Pending completion of chip pressure tolerance testing, the MW shall support regulated delivery pressures up to 350 kPa without requiring redesign and shall provide the capability to adjust pressure limits through configuration to match validated chip specifications.

**Hermetic Seal Capability**

> **IF-1.7:** The MW shall employ a standardized connection type for sample transfer that provides a hermetic seal with make/break capability and compatibility with upstream sampler and downstream chip systems.

> **IF-1.10:** The MW shall maintain a hermetic seal at the sampler-to-middleware connection during sample transfer, with zero leakage under operating pressure.

**Repeatable Connection**

> **IF-1.8 & 1.9:** The MW shall establish repeatable and reliable connections to the sampler. The breadboard implementation shall validate interface functionality, and the MW design shall incorporate features necessary to achieve ≥95% connection success over 20–30 sequential sample cycles in deployment configurations.

---

## Gas and Pneumatic Chip Interface

**Functional Purpose:** Provide pneumatic pressure to open/close on-chip valves, control fluid routing through chip channels during sample processing.

Pneumatic pressures, volumes, and channel requirements are subject to refinement as chip and MW pneumatic designs mature; the MW shall incorporate configurable and scalable pneumatic control and storage to accommodate these changes.

### Functional Requirements:

**Valve Actuation**

> **IF-2.1:** The MW shall supply sufficient pressure to reliably actuate all pneumatic valves on the chip, with a minimum actuation pressure of 175 kPa and a target operating pressure of 350 kPa.

> **IF-2.2:** The MW shall maintain pressure to keep valves in the closed state during hold periods, with valves remaining closed without leakage throughout the commanded hold duration at 175–350 kPa.

**Multi-Channel Control**

> **IF-2.4:** The MW shall independently control multiple pneumatic valve channels per chip, with a target of 2 independent channels and a maximum of 4 channels, actuating valves in any sequence without crosstalk.

**Pressure Stability**

> **IF-2.3:** The MW shall maintain stable pressure at the chip inlet manifold during valve-hold states, with pressure variation not exceeding ±1% of setpoint or ±1.5 kPa, to prevent volumetric drift, leakage, or bubble nucleation.

**Gas Volume Availability**

> **IF-2.5:** The MW shall provide sufficient gas for all valve operations within a single chip processing cycle, supporting 2–4 actuations per cycle depending on final design.

> **IF-2.6:** The MW gas supply shall account for the volume consumed per valve actuation to enable proper sizing of the gas reservoir for full deployment duration.

> **IF-2.7:** The MW shall provide total gas storage capacity sufficient for full deployment, calculated as the number of chips multiplied by actuations per chip multiplied by volume per actuation, plus an appropriate safety margin.

**Gas Cleanliness**

> **IF-2.8:** The MW shall use a clean, inert gas for the deployable configuration and may use compressed air for laboratory bench testing. Note: Current baseline gas is nitrogen (N₂).

> **IF-2.9:** The MW gas supply shall be clean and dry, free of moisture, particulates, and contaminants that could affect chip materials or reactions.

> **IF-2.10:** The MW breadboard system shall use an external gas source. The deployable system gas source (host platform integrated vs. external) shall be determined based on design requirements, with adequate pressure available from the host platform.

---

## Middleware Reagent Interface

**Functional Purpose:** Deliver processing reagents from middleware storage to chip in correct sequence, volumes and timing for sample modification

### Functional Requirements:

**Reagent Types and Storage**

> **IF-3.1:** The MW shall store and deliver a minimum of 3 and up to 5 reagent types (liquid or gas) from the Middleware Reagent Cartridge (MWRC) to the chip, with a target of 4 reagent types to support the full chip protocol.

- External chip processing requires only water; downstream analytical device sample preparation may require additional priming and wash buffers.

**Reagent Volumes, Delivery and Precision**

> **IF-3.2 & 3.4:** The MWRC shall store and deliver sufficient reagent volume for all chips in a deployment, with an initial design allocation for delivery of 550 µL (minimum), 650 µL (target) and 750 µL (maximum) with precision of ±5%. The MW shall support configurable volume and precision to accommodate future chip and delivery mechanism requirements.

- Reagent volume requirements and precision are subject to change as chip design, fluidic architecture, and delivery mechanisms are refined through ongoing development and validation.

**Sequential Delivery**

> **IF-3.3:** The MW shall deliver reagents in the order specified by the analytical chip developer protocol and shall support configurable sequencing to accommodate different chip protocols while ensuring 100% correct reagent order at each processing step.

**Contamination Prevention**

> **IF-3.5:** The MW shall prevent cross-contamination between reagent types and between sequential chip operations. Each chip shall receive clean reagents with zero carryover from prior samples.

> **IF-3.8:** All wetted surfaces in the reagent delivery path shall be constructed of materials chemically compatible with the reagents used. Note: Current approved materials include PMMA, FEP/PTFE, PEEK, EPDM, and COC/COP.

**Bubble-Free Delivery**

> **IF-3.6:** The MW shall minimize air bubbles in reagent delivery, with a preferred design goal of zero bubbles, a target bubble volume of less than 10% of the total reaction volume, and a maximum allowable of less than 20%.

> **IF-3.7:** The chip shall have standardized port positions for reagent inputs, with all ports accessible by the dock and providing repeatable alignment.

- The current design uses 4 input ports based on the established chip form factor.

> **IF-3.9:** The MW shall deliver reagents at a pressure within the chip tolerance range, with a minimum of 50 kPa, a target of 380 kPa, and a maximum of 500 kPa.

- Reagent delivery pressure limits and targets are subject to change as chip pressure tolerance and fluidic interface characteristics are refined through ongoing development and validation.

---

## Middleware and Chip Waste Management

**Functional Purpose:** Collect and isolate waste from chip processing to prevent cross-contamination and manage deployment capacity

### Functional Requirements:

**Waste Containment**

> **IF-4.1:** The MW shall collect all liquid waste generated during chip processing, with an estimated waste volume of 650 µL per chip based on total chip fluidic volume.

- Reagent volume requirements are subject to change as chip design, fluidic architecture, and delivery mechanisms are refined through ongoing development and validation.

> **IF-4.4:** The MW shall contain all waste securely without leakage over the full deployment duration. Waste containment is currently sized at 2× the chip fluidic volume.

**Waste Isolation**

> **IF-4.2:** The MW shall prevent waste from one chip from contacting waste from another chip, maintaining zero cross-contamination between sequential chip processing runs.

**Capacity Planning**

> **IF-4.3:** The MW shall provide sufficient waste storage capacity for a full deployment, with total capacity equal to or greater than the number of chips multiplied by the waste volume per chip.

---

## Middleware to Analytical Device Interface

**Functional Purpose:** Transfer processed sample (analysis ready) from middleware to Analytical Device for detection and analysis. The MW shall deliver processed samples through a standardized interface in a manner that preserves compatibility with analytical device requirements and does not interfere with analytical device operation, while downstream analytical processing remains outside the MW functional scope.

### Functional Requirements:

**Volume Delivery**

> **IF-5.1:** The MW shall deliver the precise volume required by the analytical device, with a minimum of 70 µL, a target of 100 µL, and a maximum of 130 µL.

- Reagent volume requirements are subject to change as chip design, fluidic architecture, and delivery mechanisms are refined through ongoing development and validation.

> **IF-5.2:** The modified sample output from the MW shall meet the concentration requirements of the analytical device. Note: Current reference target is a DNA concentration of 20 ng within a range of 10–30 ng.

**Buffer Compatibility**

> **IF-5.3:** The sample buffer at the MW output shall be compatible with the downstream analytical device chemistry, causing no inhibition of downstream analytical reactions.

**Contamination-Free Transfer**

> **IF-1.4-ref:** Contamination-free transfer from MW to analytical device is governed by the same contamination prevention principles defined in IF-1.4 and IF-3.5, applied to the downstream handoff. No introduction of foreign DNA/RNA shall occur during transfer to the analytical device.

**Delivery Method**

> **IF-5.4:** The MW shall transfer the processed sample to the downstream analytical device inlet. The current design accepts manual transfer, with the interface designed to accommodate future automation.

---

## Electrical (Power and Control) Interface

**Functional Purpose:** Provide electrical power to all Middleware subsystems and enable communications and control between platform, middleware and chips.

Note: The specified operating power and control specifications are based on the current host platform power bus specification and may be refined to accommodate other host platform power bus characteristics in future deployments and developments related to MW design. Current reference platform: LRAUV 3G ESP.

### Functional Requirements:

**Power Distribution**

> **IF-6.1:** The MW shall operate at a standard voltage compatible with the platform power bus, with an acceptable range of 12–48V and a target operating voltage of 14V.

> **IF-6.5:** The MW shall distribute stable electrical power to all subsystems, including thermal, pneumatic, control, and sensor systems.

**Peak Power Handling**

> **IF-6.2:** The MW shall handle peak current demand of 3–6A, driven primarily by Peltier module operation during thermal cycling.

> **IF-6.3:** The MW average power consumption per processing cycle shall fall within 30–75W, with a target of 50W, encompassing all subsystems: thermal, pneumatic, and control.

> **IF-6.4:** The MW total energy consumption per sample processing cycle (approximately 2 hours) shall be within the platform energy budget, with a target of 100–150 Wh for 20–30 samples over deployment.

**Control Communication**

> **IF-7.1:** The MW shall communicate with the host platform via a serial data/control protocol, providing reliable command and status communication.

> **IF-7.2:** The MW shall implement a defined set of control commands from the host platform to configure, start, pause, stop, and safely operate fluidic, thermal, and sensing subsystems. The command set shall include the following classes: Session and Identity, System State and Run Control, Subsystem Control, Automation and Workflow Execution, Telemetry and Monitoring, Faults, and Configuration and Diagnostics.

**Sensor Feedback**

> **IF-7.3:** The MW shall report structured status information to the host platform, including system state and run progress, thermal, fluidic, and actuator conditions, power and electrical health, and structured fault and alarm indicators, at sufficient update rate and accuracy to support supervisory control, diagnostics, and safe operation.

> **IF-7.4:** The MW shall include sensors necessary for safe and accurate thermal and fluidic operation, at minimum: a reaction temperature sensor for closed-loop PCR control, a Peltier hot-side temperature sensor for thermal protection, an ambient temperature sensor for environmental compensation, an inlet pressure sensor for fluid delivery monitoring and leak detection, valve or actuator state feedback to confirm commanded positions, and electrical supply monitoring for power integrity.

> **IF-7.6:** The MW interface connectors shall be robust and suitable for marine environments, including exposure to moisture, salt air, vibration, and temperature variation. Marine- or MIL-rated connectors are preferred where exposed; commercial connectors may be used if adequately protected within a sealed enclosure.

---

## Thermal Management Interface

**Functional Purpose:** Provide precise temperature control to chip for molecular reactions (e.g., Thermal Cycling or Isothermal Amplification)

Thermal performance and power requirements are subject to refinement as chip thermal design and protocols evolve; the MW thermal system shall incorporate sufficient margin and configurability to accommodate these changes.

### Functional Requirements:

**Temperature Range**

> **IF-9.1:** The MW shall control chip reaction temperature over a range of 35–100°C to support both PCR thermal cycling and isothermal amplification protocols.

**Temperature Precision**

> **IF-9.2:** The MW shall maintain chip temperature within ±1°C of the commanded setpoint during molecular reactions.

**Ramp Rate**

> **IF-9.3:** The MW shall change chip temperature at a rate of 1–5°C/sec to support thermal cycling for PCR protocols.

**Temperature Uniformity**

> **IF-9.4:** The MW shall achieve temperature uniformity across the chip reaction zone with variation not exceeding ±1°C, preventing hot or cold spots that could affect reaction efficiency.

**Thermal Cycling**

> **IF-9.5:** The MW shall support PCR thermal cycling by repeatedly cycling through denaturation, annealing, and extension temperatures for 25–40 cycles with stable performance across all cycles.

> **IF-9.7:** The MW shall maintain each commanded temperature for the required dwell time, holding within ±0.5°C of setpoint for at least 95% of the commanded dwell duration.

**Isothermal Hold**

> **IF-9.6:** The MW shall maintain a constant temperature for isothermal amplification reactions (e.g., CRISPR-based assays) for a duration of 30–60 minutes with stable temperature throughout the reaction period.

**Thermal Contact, Isolation, and Power**

> **IF-9.8:** The MW–chip interface shall provide an effective thermal contact resistance (interface plus contact stack) of 0.5–1.0 K/W or less over the reaction footprint, sufficient to achieve a heating ramp of at least 2°C/s, a cooling ramp of at least 1°C/s, and a steady-state error of 0.5°C or less at 60°C and 95°C under worst-case ambient conditions.

> **IF-9.9:** The MW shall thermally isolate the PCR chip such that environmental temperature variations do not materially affect reaction temperature accuracy, uniformity, or thermocycling performance. The system shall meet PCR performance requirements while ambient temperature is within 5–38°C.

> **IF-9.10:** The MW shall remove heat from the Peltier hot side such that the cold side (chip) can achieve and maintain specified PCR temperatures and ramp rates under worst-case operating conditions.

> **IF-9.11:** The thermal control subsystem shall operate within a power budget of 20–75W, with a target of 30–50W, accounting for temperature range and cycling demands.

---

## Mechanical Docking (Middleware to Chip)

**Functional Purpose:** Physically secure chip in position and create all physical (fluidic, pneumatic, electrical, thermal) connections between Middleware and chip.

Docking geometry and interface requirements are subject to refinement as chip and interface designs evolve; the MW docking system shall incorporate sufficient tolerance, adjustability, and modularity to accommodate these changes.

### Functional Requirements:

**Chip Retention**

> **IF-11.1:** The MW dock shall accommodate a standardized chip with dimensions of approximately 88 × 30 × 3 mm (L × W × H), with all chips fitting in the dock without interference. Exact dimensions and tolerances per chip developer technical drawings.

> **IF-11.2:** The MW dock retention mechanism shall account for chip mass plus operational and dynamic forces including acceleration loads.

> **IF-11.5:** The MW shall hold the chip securely in position throughout the entire processing cycle, preventing any movement during fluid delivery, thermal cycling, and pneumatic actuation.

> **IF-11.10:** The MW dock shall be designed for compatibility with the chip substrate material, accounting for material properties relevant to sealing, thermal contact, and mechanical handling. Note: Current chip substrate is PMMA.

> **IF-11.11:** The chip shall withstand the mechanical loads imposed by the MW dock during processing, with a maximum operating pressure of 0.5 MPa without damage.

**Hermetic Sealing**

> **IF-11.6:** The MW dock shall create leak-proof seals at all fluidic and pneumatic connections to the chip, achieving zero leakage under operating pressure.

> **IF-11.7:** The force required to achieve a hermetic seal shall not exceed 0.5 MPa compressive stress and shall not damage the chip, with a target sealing pressure of 0.3 MPa and a minimum of 0.1 MPa.

**Alignment**

> **IF-11.3:** The MW dock shall align chip ports with middleware connections based on exact port positions as defined in chip developer interface control drawings for repeatable connection across all docking cycles.

> **IF-11.8:** The MW dock shall achieve automatic chip alignment within ±0.08 mm using alignment features (pins, grooves, or equivalent), ensuring all fluidic and pneumatic connections are properly registered.

> **IF-11.4:** The port geometry (threaded, barbed, open hole, or other) shall be compatible with the dock connection method. Port type selection is design-dependent and shall be jointly determined.

**Connection/Disconnection Reliability**

> **IF-11.9:** The MW dock shall make connections reliably when docked and break cleanly when undocked, achieving a connection success rate of at least 95% (target 98%) over 20–30 sequential docking cycles.
