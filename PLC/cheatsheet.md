

| Bits | Two's Complement Min | Two's Complement Max | Positive Min | Positive Max |
|------|----------------------|----------------------|--------------|--------------|
| 16   | -32,768              | 32,767               | 0            | 65,535      |
| 15   | -16,384              | 16,383               | 0            | 32,767      |
| 14   | -8,192               | 8,191                | 0            | 16,383      |


- **HMI Libraries**:  
  The path for HMI Libraries is:
  ```bash
  C:\TwinCAT\Functions\TE2000-HMI-Engineering\References
  ```

- **Build a Newget package in TXAEShell**:
  1. Select the project (e.g: ProcessAutomationLib)
  2. Right Click
  3. Select `Create NuGet Package`
  4. Once Finished. you can find the built library at `C:\TwinCAT\Functions\TE2000-HMI-Engineering\References`

- **Add Route**:
  1. Click on `Twincat Config Mode` icon in hidden icons
  2. `Router` --> `Edit Routes`
  3. `Add` --> `Advanced Settings`
  4. Choose `Transport Type` --> `TCP_IP`
  5. Choose` Address Info` --> `IP Address`
  6. Click in `Broadcast Search`
  7. Choose appropriate adaptor / network interface on your computer, wifi/pci etc. press `OK`
  8. Window displays all found twincat machines
  9. Select the desired twincat machine --> click on `Add Route`
  10. New windows `Add Remote Route` appears and you need add `Remote User Credential` like `User` and `Password` --> click `OK`
  11. You should see the connected icon (lock) in the list
 
- **Load solution from target**:
  1. Open Twincat XAE Shell
  2. File --> open --> Open Project from Target
  3. Add Route if it does not exsists.
  4. Select the appropriate `Target system` --> `OK`
  5. A windows might be displayed wiht warning message, if there is a version mismatch. click on `OK`
  6. A windows appears to choose the location to save the solution. Create a folder and choose it. `Select Folder`
  7. Warning message might pop up, if there is an architecture miss match. click `YES`
  8. The solution is loaded and also located at the appopriate location, selected before.

- **Save solution from target**:
  1. Load solution from target
  2. Right click on the `Solution(Solution 'Atlant3D' (1 project))` -->  `Save <project> as Archive`
 
- **Find Compiler version**:
  1. Right click on the` PLC Project (N0_PLC_Project)` --> `compiler` --> `Solution options` --> `Compiler Version ` --> `Drop down Menu`
 
- **Pin Compiler Version**:
  1. 
