
## 1  Original question  
> *“I have a bubbler with some material inside it. I am using it for the deposition process (ALD).  
> The amount of material coming out depends on the vapour pressure maintained in the bubbler.  
> Tell me the relationship between the vapour pressure and the material coming out of the bubbler.  
> Are they directly proportional or inversely proportional? Any appropriate formula if you can.”*

---

### 1.1  Answer  

For an **ideal, fully‑saturated bubbler** the molar flow of precursor that exits with the carrier gas is  

\\[
\\dot n_{\\text{prec}} \\,=\\,
\\dot n_{\\text{carrier}}\\,
\\frac{P_{\\text{vap}}}{P_{\\text{tot}}-P_{\\text{vap}}}
\\quad\\text{(Eq. 1)}
\\]

| Symbol | Meaning |
|--------|---------|
| `P_vap` | Equilibrium vapour‑pressure of the precursor at bubbler temperature |
| `P_tot` | Total pressure inside the bubbler (vapour + carrier) |
| `\\dot n_{carrier}` | Carrier‑gas molar flow (mol s⁻¹) |
| `\\dot n_{prec}` | Precursor molar flow (mol s⁻¹) |

When `P_vap  ≪  P_tot` (the normal ALD case)  

\\[
\\dot n_{\\text{prec}} \\approx
\\dot n_{\\text{carrier}}\\,
\\frac{P_{\\text{vap}}}{P_{\\text{tot}}}
\\quad\\text{(Eq. 1a)}
\\]

so the delivery rate is **directly proportional to `P_vap`** (and inversely proportional to `P_tot`).  

If the carrier flow is measured volumetrically at the bubbler temperature `T`,  

\\[
\\dot n_{\\text{prec}} = Q_{\\text{carrier}}\\,\\frac{P_{\\text{vap}}}{RT}
\\quad\\text{(Eq. 2)}
\\]

where `R` is the universal gas constant.

#### 1.1.1  Derivation  
1. Head‑space equilibrium: \\( p_{prec} = P_{vap} \\)  
2. Dalton’s law: \\( p_{carrier} = P_{tot} - P_{vap} \\)  
3. Mole fraction ratio: \\( x_{prec}/x_{carrier} = P_{vap}/(P_{tot}-P_{vap}) \\)  
4. Steady‑state mol balance gives Eq. 1.

---

### 1.2  Practical implications  

| **How you change the bubbler** | **What Eq. 1 predicts** |
|--------------------------------|-------------------------|
| Raise bubbler **temperature** | `P_vap` rises exponentially → delivery rises exponentially |
| Lower **total/head‑space pressure** | Denominator shrinks → delivery rises strongly |
| Increase **carrier‑gas flow** | `\\dot n_{prec}` rises linearly; concentration stays constant |
| Let liquid level drop or clogging occur | Bubbles may not reach equilibrium → Eq. 1 over‑predicts |
| `P_vap` → `P_tot` | Eq. 1 diverges; two‑phase flow dominates |

---

## 2  Follow‑up questions  
> *“Since you mentioned vapour pressure and carrier pressure: Are they independent of each other?  
> Does the vapour pressure depend only on bubbler temperature?  
> How about the relationship between carrier pressure and the bubbler material?”*

---

### 2.1  Answer  

#### 2.1.1  Independence  
* **Vapour pressure `P_vap`** is an **equilibrium property of the precursor**. For a pure substance it depends **only on temperature** (Antoine/Clausius–Clapeyron).  
* **Carrier‑gas pressure `P_carrier`** is set by the external plumbing (MFCs, valves, pump).  
Because the inert carrier gas is practically insoluble and non‑reactive, the two pressures are **independent** except at very high total pressures.

#### 2.1.2  Temperature dependence of `P_vap`  

For a pure precursor:  

\\[
\\log_{10} P_{\\text{vap}} = A - \\frac{B}{T+C}
\\]

where `A, B, C` are Antoine constants.  
For mixtures, Raoult’s law applies and composition also matters.

#### 2.1.3  Effect of carrier pressure on delivery  

Start again from Eq. 1 with `P_tot = P_carrier + P_vap`.

| Change | Effect on mole fraction \\(x_{prec} = P_{vap}/P_{tot}\\) | Consequence |
|--------|-----------------------------------------------------------|-------------|
| **Increase `P_carrier`** | Dilutes precursor | `\\dot n_{prec}` decreases |
| **Decrease `P_carrier`** | Enriches precursor | `\\dot n_{prec}` increases |
| **Raise temperature** (fixed pressure) | Increases `P_vap` → increases `x_{prec}` | Exponential rise in delivery |

For the usual **dilute limit** (`P_vap ≪ P_tot`)  

\\[
\\dot n_{\\text{prec}} \\approx \\dot n_{\\text{carrier}}\\,
\\frac{P_{\\text{vap}}}{P_{\\text{tot}}}
\\]

so the delivery is **directly proportional to `P_vap`** and **inversely proportional to `P_tot`**.

---

### 2.2  Design rule‑of‑thumb  

> **Any change that doubles `P_vap` roughly doubles the precursor molar flow, provided you do not simultaneously double `P_tot`.**

---

## 3  Key Take‑aways  

1. **Independent knobs**  
   * `Temperature → P_vap`  
   * `Pressure / flow → P_carrier`, `\\dot n_{carrier}`  
2. In the outlet stream the two pressures couple through **Dalton’s law** (Eq. 1).  
3. Over normal ALD conditions delivery is  
   * **∝ `P_vap`** (direct)  
   * **∝ 1/`P_tot`** (inverse)

With Eq. 1 and the precursor’s Antoine constants you can predict how changing temperature, carrier‑gas flow, or pressure shifts the dose reaching the wafer—until non‑ideal effects (entrainment, decomposition) begin to dominate.

