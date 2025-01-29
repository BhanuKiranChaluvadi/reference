# 🛑 Stop Categories According to IEC 60204-1

In industrial automation, different stop categories ensure **safe machine stopping** under various conditions. Below is a simplified explanation of **Stop Categories 0, 1, and 2** as per **IEC 60204-1**.

## 🚦 Stop Category Table

| **Stop Category** | **Description** | **Power to Motor?** | **Example Usage** |
|------------------|----------------|--------------------|------------------|
| **Category 0** (Emergency Stop) | **Immediate stop** by cutting power. The machine coasts to a stop unless mechanical braking is applied. | ❌ **Power is immediately removed.** | Emergency stop button (E-Stop), safety relay triggering. |
| **Category 1** (Controlled Stop) | **Stops the machine with controlled deceleration** before cutting power. | ✅ **Power remains** during stopping, then is removed. | Safe machine shutdown, controlled deceleration before power-off. |
| **Category 2** (Operational Stop) | **Stops with controlled deceleration but keeps power to the motor** (for holding torque or quick restart). | ✅ **Power remains ON** even after stopping. | CNC machines holding position, robotic arms waiting for resume command. |

## ⚡ Additional Stop Types
- **Safe Torque Off (STO)** → Removes torque **without cutting full power** (used in safety circuits).
- **Coast-to-Stop** → The motor stops naturally with **no braking**.
- **Dynamic Braking Stop** → Uses resistors to slow down **faster than coasting**.

## 🔹 Summary
- **Category 0** → **Immediate power cut-off** (Emergency Stop 🚨).
- **Category 1** → **Controlled stop before power-off** (Deceleration ⏬).
- **Category 2** → **Controlled stop with power retained** (Holding Torque ✅).

