# Bubbler Vapour‑Pressure & Precursor Delivery in ALD – Complete Discussion

## 1  Original question  
> *“I have a bubbler with some material inside it. I am using it for the deposition process (ALD).  
> The amount of material coming out depends on the vapour pressure maintained in the bubbler.  
> Tell me the relationship between the vapour pressure and the material coming out of the bubbler.  
> Are they directly proportional or inversely proportional? Any appropriate formula if you can.”*

---

### 1.1  Answer  

For an **ideal, fully‑saturated bubbler** the molar flow of precursor that exits with the carrier gas is  

$$
\dot n_{\text{prec}} = 
\dot n_{\text{carrier}}
\frac{P_{\text{vap}}}{P_{\text{tot}} - P_{\text{vap}}}
\quad \text{(Eq. 1)}
$$

| Symbol | Meaning |
|--------|---------|
| $P_{\text{vap}}$ | Equilibrium vapour‑pressure of the precursor at bubbler temperature |
| $P_{\text{tot}}$ | Total pressure inside the bubbler (vapour + carrier) |
| $\dot n_{\text{carrier}}$ | Carrier‑gas molar flow (mol s⁻¹) |
| $\dot n_{\text{prec}}$ | Precursor molar flow (mol s⁻¹) |

When $P_{\text{vap}} \ll P_{\text{tot}}$ (the normal ALD case):  

$$
\dot n_{\text{prec}} \approx 
\dot n_{\text{carrier}}
\frac{P_{\text{vap}}}{P_{\text{tot}}}
\quad \text{(Eq. 1a)}
$$

so the delivery rate is **directly proportional to $P_{\text{vap}}$** (and inversely proportional to $P_{\text{tot}}$).  

If the carrier flow is measured volumetrically at the bubbler temperature $T$,  

$$
\dot n_{\text{prec}} = Q_{\text{carrier}} \cdot \frac{P_{\text{vap}}}{RT}
\quad \text{(Eq. 2)}
$$

where $R$ is the universal gas constant.

#### 1.1.1  Derivation  
1. Head‑space equilibrium: $p_{\text{prec}} = P_{\text{vap}}$  
2. Dalton’s law: $p_{\text{carrier}} = P_{\text{tot}} - P_{\text{vap}}$  
3. Mole fraction ratio: $x_{\text{prec}} / x_{\text{carrier}} = P_{\text{vap}} / (P_{\text{tot}} - P_{\text{vap}})$  
4. Steady‑state mol balance gives Eq. 1.

---

### 1.2  Practical implications  

| **How you change the bubbler** | **What Eq. 1 predicts** |
|--------------------------------|-------------------------|
| Raise bubbler **temperature** | $P_{\text{vap}}$ rises exponentially → delivery rises exponentially |
| Lower **total/head‑space pressure** | Denominator shrinks → delivery rises strongly |
| Increase **carrier‑gas flow** | $\dot n_{\text{prec}}$ rises linearly; concentration stays constant |
| Let liquid level drop or clogging occur | Bubbles may not reach equilibrium → Eq. 1 over‑predicts |
| $P_{\text{vap}} \to P_{\text{tot}}$ | Eq. 1 diverges; two‑phase flow dominates |

---

## 2  Follow‑up questions  
> *“Since you mentioned vapour pressure and carrier pressure: Are they independent of each other?  
> Does the vapour pressure depend only on bubbler temperature?  
> How about the relationship between carrier pressure and the bubbler material?”*

---

### 2.1  Answer  

#### 2.1.1  Independence  
* **Vapour pressure $P_{\text{vap}}$** is an **equilibrium property of the precursor**. For a pure substance it depends **only on temperature** (**Antoine/Clausius–Clapeyron**).  
* **Carrier‑gas pressure $P_{\text{carrier}}$** is set by the external plumbing (MFCs, valves, pump).  
Because the inert carrier gas is practically insoluble and non‑reactive, the two pressures are **independent** except at very high total pressures.

#### 2.1.2  Temperature dependence of $P_{\text{vap}}$  

For a pure precursor:  

$$
\log_{10} P_{\text{vap}} = A - \frac{B}{T + C}
$$

where $A$, $B$, and $C$ are Antoine constants.  
For mixtures, **Raoult’s law** applies and composition also matters.

#### 2.1.3  Effect of carrier pressure on delivery  

Start again from Eq. 1 with $P_{\text{tot}} = P_{\text{carrier}} + P_{\text{vap}}$.

| Change | Effect on mole fraction $x_{\text{prec}} = P_{\text{vap}} / P_{\text{tot}}$ | Consequence |
|--------|--------------------------------------------------------------------------|-------------|
| **Increase $P_{\text{carrier}}$** | Dilutes precursor | $\dot n_{\text{prec}}$ decreases |
| **Decrease $P_{\text{carrier}}$** | Enriches precursor | $\dot n_{\text{prec}}$ increases |
| **Raise temperature** (fixed pressure) | Increases $P_{\text{vap}} \Rightarrow x_{\text{prec}}$ increases | Exponential rise in delivery |

For the usual **dilute limit** ($P_{\text{vap}} \ll P_{\text{tot}}$):  

$$
\dot n_{\text{prec}} \approx 
\dot n_{\text{carrier}}
\frac{P_{\text{vap}}}{P_{\text{tot}}}
$$

so the delivery is **directly proportional to $P_{\text{vap}}$** and **inversely proportional to $P_{\text{tot}}$**.

---

### 2.2  Design rule‑of‑thumb  

> **Any change that doubles $P_{\text{vap}}$ roughly doubles the precursor molar flow, provided you do not simultaneously double $P_{\text{tot}}$.**

---

## 3  Key Take‑aways  

You control the precursor delivery by adjusting two independent knobs:

1. **Bubbler temperature**  
   → sets the **precursor vapour pressure** $P_{\text{vap}}$ via the Antoine equation.

2. **Carrier-gas flow and system pressure**  
   → set the **carrier pressure** $P_{\text{carrier}}$ and the **molar flow** $\dot n_{\text{carrier}}$.

These independently affect how much precursor vapor is delivered:

- In the outlet stream, precursor and carrier couple through **Dalton’s law** using Eq. 1.
- Under normal ALD conditions, delivery is:
  - $\propto P_{\text{vap}}$ (directly proportional)
  - $\propto \frac{1}{P_{\text{tot}}}$ (inversely proportional)

With Eq. 1 and the precursor’s Antoine constants, you can predict how changing temperature, carrier-gas flow, or pressure affects precursor dose — until real-world issues like entrainment or decomposition take over.
