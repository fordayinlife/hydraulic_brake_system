# Vacuum-Assisted Hydraulic Brake System & ABS — Interactive Cutaway

An interactive, single-file HTML5/SVG engineering schematic and real-time 60 FPS physics simulation of an automotive **Vacuum-Assisted Hydraulic Brake System with Anti-Lock Braking System (ABS)**.

Designed as a self-contained educational and diagnostic visualization, this application animates every pneumatic, mechanical, hydraulic, and electronic stage from driver foot input at the brake pedal to dual-pad clamping on vented disc rotors.

---

## Key Features

### 1. Color-Coded Fluid, Pneumatic & Signal Pathways
Every tube, chamber, and wiring harness in the CAD cutaway is color-coded with animated flow indicators:
* **Cyan (`4.8 PSI` / $\approx 20\text{ inHg}$):** Engine intake manifold vacuum, spring-loaded one-way check valve, and the booster's constant-vacuum front chamber.
* **Amber (`14.7 PSI`):** Atmospheric air entering through the rear dust boot/filter into the booster control chamber when the brake pedal is depressed.
* **Crimson / Rose (`0 – 1,450 PSI`):** Incompressible DOT 4 brake fluid traveling through independent Primary (front) and Secondary (rear) hydraulic circuits, the ABS modulator galleries, and caliper bores.
* **Emerald (`Digital Pulses`):** Hall-effect Wheel Speed Sensor (WSS) signal harnesses reading toothed reluctor tone rings on both front and rear hubs.

### 2. Seven Animated Cutaway Subsystems
1. **Brake Pedal Lever & Input Pushrod:** Pivoting firewall fulcrum ($\approx 4:1$ mechanical advantage) driving a clevis-pinned pushrod linearly into the booster control valve.
2. **Engine Intake Manifold & One-Way Check Valve:** Spring-loaded flapper valve that opens to evacuate air during pedal release and seals vacuum inside the drum under load.
3. **Vacuum Brake Booster:** Cutaway stamped-steel drum with a rolling rubber diaphragm, internal return springs, vacuum port plunger, atmospheric air valve, and rubber reaction disc delivering a $3.5\times$ force assist multiplier.
4. **Tandem Master Cylinder & Fluid Reservoir:** Translucent reservoir with `MAX`/`MIN` indicators, dual-circuit safety baffle, dynamic meniscus level, float sensor, and Primary (`PRI`) / Secondary (`SEC`) pistons with return springs.
5. **ABS Hydraulic Control Unit (HCU) & ECU:** Cutaway valve block featuring Normally-Open Inlet Solenoids (`IN-1`, `IN-2`), Normally-Closed Outlet Dump Solenoids (`OUT-1`, `OUT-2`), a rotating eccentric-cam electric Return Pump, and a spring-loaded Low-Pressure Accumulator.
6. **Front Floating Disc Brake Assembly (Primary Circuit):** Handles $\approx 70\%$ of braking bias with a spinning vented rotor, dynamic thermal heat glow, toothed ABS tone ring, extending inner piston, and sliding caliper bridge clamping both inner and outer pads.
7. **Rear Floating Disc Brake Assembly (Secondary Circuit):** Independent rear circuit ($\approx 30\%$ bias) with integrated ABS tone ring and wheel speed sensor.

### 3. Live Telemetry & Component Inspector
* **Real-Time Telemetry Strip:** Continuously tracks **Pedal Force ($\text{N}$)**, **Booster Assist ($+\text{N}$)**, **Rear Chamber Pressure ($\text{PSI}$)**, **Line Hydraulic Pressure ($\text{PSI}$)**, **Wheel Speed ($\text{MPH}$)**, and **ABS Valve State**.
* **Interactive Inspector Drawer:** Click any component directly on the schematic (or step through Stages 1–7) to view engineering explanations and component-specific live metrics.

---

## Controls & Shortcuts

| Control | Action |
| :--- | :--- |
| **Press / Latch Brake Pedal** | **Short Click ($< 250\text{ ms}$):** Latches the brake pedal ON at $85\%$ for hands-free inspection.<br>**Press & Hold:** Applies $90\%$ braking momentarily until released. |
| **`SPACE` Bar** | Hold to apply $100\%$ braking force; release to evacuate vacuum and return pedal. |
| **Click Pedal on Schematic** | Toggles the brake pedal latch directly on the SVG diagram. |
| **Brake Pedal Travel Slider** | Manually scrub pedal depression anywhere between $0\%$ and $100\%$. |
| **Vehicle / Rotor Speed Slider** | Adjust wheel rotation speed from $0\text{ MPH}$ to $100\text{ MPH}$ (or click **Cruise 65 MPH**). |
| **Auto-Demo Loop** | Runs an automated 11-second showcase cycling through vacuum cruise, progressive normal braking, icy-road $12\text{ Hz}$ ABS modulation, and pedal release. |
| **Ice / Wet Surface Toggle** | Lowers tire-road friction so heavy braking ($> 55\%$) triggers $12\text{ Hz}$ ABS `APPLY` / `HOLD` / `DUMP` solenoid pulsing. |
| **Auto-Accelerate on Release** | Smoothly accelerates the rotors back up to $65\text{ MPH}$ after the brake pedal is released. |

---

## Engineering & Physics Model

The simulation computes real-time pneumatic and hydraulic equilibrium at 60 FPS:

* **Booster Pressure Differential ($\Delta P$):**
  $$\Delta P = P_{\text{rear}} - P_{\text{front}}$$
  where $P_{\text{front}} = 4.8\text{ PSI}$ (constant manifold vacuum) and $P_{\text{rear}}$ transitions linearly from $4.8\text{ PSI}$ at rest to $14.7\text{ PSI}$ (atmospheric pressure) as the air valve opens.

* **Total Master Cylinder Pushrod Force ($F_{\text{total}}$):**
  $$F_{\text{total}} = F_{\text{pedal}} + F_{\text{boost}}$$
  with a nominal $3.5\times$ vacuum diaphragm assist ratio ($F_{\text{boost}} = 3.5 \cdot F_{\text{pedal}}$ up to booster runout).

* **Hydraulic Line Pressure ($P_{\text{line}}$):**
  $$P_{\text{line}} = \frac{F_{\text{total}}}{A_{\text{bore}}}$$
  generating up to $1,450\text{ PSI}$ in normal pass-through mode, or oscillating between $420\text{ PSI}$ and $800\text{ PSI}$ at $12\text{ Hz}$ when ABS modulation is active.

---

## Getting Started

No build tools, package managers, or backend servers are required.

1. Download or save `brake_booster_system.html`.
2. Open `brake_booster_system.html` directly in any modern web browser (Chrome, Edge, Firefox, or Safari).
3. *(Optional)* Serve via a local static server:
   ```bash
   python3 -m http.server 8080
   ```
   Then navigate to `http://localhost:8080/brake_booster_system.html`.

---

## Tech Stack & Architecture

* **Markup & Vector Graphics:** Semantic HTML5 with an inline `1480 × 780` responsive CAD-style `<svg>` schematic.
* **Styling:** [Tailwind CSS](https://tailwindcss.com/) (CDN) with `Inter` and `JetBrains Mono` typography.
* **Simulation Engine:** Self-contained Vanilla JavaScript (`requestAnimationFrame` delta-time loop) driving SVG transforms, dynamic spring geometry paths, stroke-dashoffset fluid/vacuum particle flow, and DOM telemetry updates.
