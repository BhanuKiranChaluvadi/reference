# LQR Controller Design and Real-World Implementation for a Two-Zone Heating System

This guide walks through the full development of a Linear Quadratic Regulator (LQR) for a thermal system with two heaters and two temperature zones. It includes experimental modeling, system identification, controller design, and real-world deployment tips.

---

## 🎯 System Overview

* **Zone 1** (T1): Heated by Heater 1
* **Zone 2** (T2): Heated by Heater 2
* Both zones are thermally coupled due to conduction/radiation
* Control goal: Raise both temperatures to a setpoint while keeping them close to each other and minimizing heater usage

---

## 🧪 Experiments for System Identification

### **Experiment 1**: Heater 1 ON (10%), Heater 2 OFF

* Measure T1 (direct) and T2 (coupling)
* Derive:

  * Gain: `K1`
  * Time constant: `tau1`
  * Coupling gain: `K12`

### **Experiment 2**: Heater 2 ON (10%), Heater 1 OFF

* Measure T2 (direct) and T1 (coupling)
* Derive:

  * Gain: `K2`
  * Time constant: `tau2`
  * Coupling gain: `K21`

### **Experiment 3**: Both Heaters ON (10%)

* Validate combined model behavior and superposition assumptions

---

## 📐 System Parameters

From the experiments, suppose we derive:

```python
K1 = 0.7713     # Heater 1 effect on Zone 1
tau1 = 1355.64
K12 = 0.7447    # Heater 1 effect on Zone 2

K2 = 0.3820     # Heater 2 effect on Zone 2
tau2 = 1523.04
K21 = 0.3652    # Heater 2 effect on Zone 1
```

---

## 🧠 State-Space Model

Let:

* `x1 = T1 - T_set`
* `x2 = T2 - T_set`
* `u1, u2`: PWM duty cycle (0–1)

### A Matrix (natural thermal decay):

```python
A = np.array([
    [-1/tau1,      0     ],
    [    0   ,  -1/tau2  ]
])
```

### B Matrix (heater effects):

```python
B = np.array([
    [ K1,   K21 ],
    [ K12,  K2  ]
])
```

---

## 🎯 LQR Cost Function

We minimize:

$J = \int_0^\infty (x^T Q x + u^T R u) dt$

### Q Matrix (state penalty):

```python
Q = np.array([
    [1, -0.9],
    [-0.9, 1]
])
```

* The diagonal terms penalize deviation of T1 and T2 from the setpoint.
* The off-diagonal terms penalize temperature difference (anti-symmetry).

Higher values in `Q` make the controller more aggressive in correcting temperature errors.

### R Matrix (input penalty):

```python
R = np.array([
    [0.01, 0],
    [0, 0.01]
])
```

* Penalizes high duty cycles.
* Larger values make the controller more conservative (uses less energy).

---

## 🧮 Solve the LQR Problem

### Riccati Equation:

We solve the **Continuous-time Algebraic Riccati Equation (CARE)**:

$A^T P + P A - P B R^{-1} B^T P + Q = 0$

This gives matrix `P`, which helps derive the optimal gain `K`:

### Compute Gain K:

```python
from scipy.linalg import solve_continuous_are

P = solve_continuous_are(A, B, Q, R)
K = np.linalg.inv(R) @ B.T @ P
```

### Interpretation of Matrix P:

* Matrix `P` is like a "cost-to-go" function.
* It encodes how much future penalty you'll incur if you're at state `x` now.
* Larger `P` values reflect more aggressive effort to bring the state to zero.

---

## ⚙️ Control Law

Control input:

```python
u = -K @ x
```

Where:

* `x = [T1 - T_set, T2 - T_set]`
* `u = [u1, u2]` are duty cycles (capped later)

---

## 🧪 Simulation with Duty Cycle Clipping

```python
def simulate_lqr(A, B, K, x0, T_set, dt=1.0, total_time=3600):
    n_steps = int(total_time / dt)
    x = np.array(x0, dtype=np.float64)
    x_log = []
    u_log = []
    max_duty = 0.5  # 50% max
    for _ in range(n_steps):
        u = -K @ x
        u = np.clip(u, 0, max_duty)
        x_dot = A @ x + B @ u
        x += x_dot * dt
        x_log.append(x + T_set)
        u_log.append(u)
    return np.array(x_log), np.array(u_log)
```

---

## 🛠 Real-World Implementation

### Inputs:

* T1, T2: Measured temperatures
* T\_set: Desired temperature setpoint

### Real-world control loop:

```python
x = np.array([T1 - T_set, T2 - T_set])
u = -K @ x
u = np.clip(u, 0, 0.5)

apply_pwm(heater_1, u[0])
apply_pwm(heater_2, u[1])
```

### PWM Example (5 sec period):

* ON time = `u[i] * 5`
* OFF time = `5 - ON time`

---

## ❓ What About Clipping?

If you clip after computing `u = -Kx`, then:

* You violate LQR's assumptions
* The penalty matrix `R` no longer fully governs behavior

### Solutions:

1. **Tighten R** → reduce u magnitude naturally
2. **Use MPC** → handles constraints during optimization
3. **Anti-windup logic** → handles saturation more gracefully

---

## ✅ Conclusion

* You now have a complete LQR controller for your thermal system
* You understand both theory and real-world application challenges
* You can simulate, tune, and deploy it with PWM constraints
* You understand the influence of `Q`, `R`, and the Riccati solution `P`

Let me know if you'd like a version for constrained MPC or microcontroller integration!
