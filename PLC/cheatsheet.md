

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
