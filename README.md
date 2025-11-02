# DrainPower: Drain Water Heat Pump (DWHP) Project

This repository contains the code, analysis, and final deliverables for the **DrainPower** project. This was a capstone project for the ESADE Management and Entrepreneurship course, combining technical engineering design with a comprehensive business plan.

## 💡 The Concept

DrainPower is a system designed to recover and recycle the significant thermal energy that is usually lost in residential and commercial sewage systems.

The core of the project is the **Drain Water Heat Pump (DWHP)**, a technology that can achieve an exceptional **Coefficient of Performance (COP) of up to 4.5 (450% efficiency)**. It is designed to provide a sustainable and cost-effective solution for water heating, even in colder climates, by harnessing the relatively stable temperature of drain water.

This project was not just a technical exercise but also a complete business proposal. The 'DrainPower' concept was built on the idea of a diverse (6 nationalities) engineering team targeting the commercial and residential building market, where rising energy costs and sustainability regulations create a strong demand for high-efficiency solutions.

## 📂 Project Files

This repository contains the core components of the DrainPower project:

* **`[code/drainpower_simulation.ipynb]`(./code/drainpower_simulation.ipynb)**: The Python notebook (detailed below) used to model the thermodynamic performance of the heat pump.
* **`[report/DrainPower_Final_Report.pdf]`(./report/DrainPower_Final_Report.pdf)**: The final project report, which includes the technical analysis, market research, and business plan.
* **`[presentation/DrainPower_Final_Presentation.pptx]`(./presentation/DrainPower_Final_Presentation.pptx)**: The final presentation and pitch deck for the project.
* **`[report/latex/]`(./report/latex/)**: The source LaTeX files for the final report.

---

## 💻 Technical Simulation: `drainpower_simulation.ipynb`

The core of this project is a Python-based simulation to model the performance of the DWHP. The simulation is performed in a Jupyter Notebook and relies heavily on the **[CoolProp](http://coolprop.org/)** library for accurate, real-fluid thermodynamic properties.

The notebook is structured in three cells, showing the progression from a simple concept to a realistic, optimized model.

### Cell 3: The Realistic Performance Model (Final)

This is the core of the simulation. It models a complete vapor-compression heat pump cycle using **R290 (Propane)** as the refrigerant and includes several real-world considerations.

**Function:** `calculate_realistic_performance`

**Purpose:** This function simulates the complete heat pump cycle to find the optimal refrigerant mass flow rate that **maximizes the Coefficient of Performance (COP)** for a given set of operating temperatures.

**Key Parameters:**
* `source_temp`: Temperature of the incoming drain water (°C).
* `dest_temp`: Target temperature of the hot water tank (e.g., 60°C).
* `compressor_efficiency`: The isentropic efficiency of the compressor (e.g., 0.75 - 0.85).
* `evaporator_approach` & `condenser_approach`: Realistic temperature differences (e.g., 5K) needed for heat transfer to occur in the heat exchangers.
* `superheat_K`: A safety margin (e.g., 3K) to ensure only gas enters the compressor.
* `suction_line_pressure_drop_pa` & `discharge_line_pressure_drop_pa`: Simulates pressure loss from friction in the pipes.

**Thermodynamic Cycle Simulation:**
The function mathematically simulates the four key stages of the heat pump cycle:
1.  **State 1 -> 2 (Compression):** The cool, low-pressure gas is compressed, becoming a hot, high-pressure gas. The simulation accounts for the compressor's inefficiency.
2.  **State 2 -> 3 (Condensation):** The hot gas releases its heat to the destination water, condensing into a high-pressure liquid.
3.  **State 3 -> 4 (Expansion):** The high-pressure liquid passes through an expansion valve, causing its pressure and temperature to drop.
4.  **State 4 -> 1 (Evaporation):** The cold, low-pressure liquid absorbs heat from the warm drain water and boils back into a gas, completing the cycle.

**Outputs:**
The main script runs this simulation across a range of source temperatures (10°C to 30°C) and generates:
1.  A plot of **COP vs. Source Temperature**, showing how efficiency improves with warmer drain water.
2.  A plot of the **optimal refrigerant flow rate** for each condition.
3.  An **Enthalpy-Entropy (P-h) diagram** for the base case (20°C) to visualize the thermodynamic cycle.
4.  A printout of key performance metrics (COP, Heat Delivered, etc.) for the base case.

### Cells 1 & 2: Earlier Drafts

These cells are included to show the project's development.
* **Cell 1:** A highly simplified conceptual model using basic specific heat equations.
* **Cell 2:** An intermediate step that used CoolProp but had several logical errors.
