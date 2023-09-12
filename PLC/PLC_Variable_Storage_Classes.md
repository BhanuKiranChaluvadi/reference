# PLC Variable Storage Classes (IEC 61131-3)

| Storage Class   | Lifetime & Accessibility                              | Use                                                                                                       |
|-----------------|------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| `VAR`           | Exists during one PLC cycle. Local accessibility.    | Temporary values or intermediate calculations.                                                            |
| `VAR_INPUT`     | Updated each PLC cycle. Read-only.                   | Receive values from outside the program or function block.                                                |
| `VAR_OUTPUT`    | Retained between PLC cycles. Write-only.             | Send values outside the program or function block.                                                        |
| `VAR_IN_OUT`    | Retained between PLC cycles. Read & Write.           | Bidirectional data exchange.                                                                              |
| `VAR_GLOBAL`    | Retained between PLC cycles. Global accessibility.   | Values shared across multiple programs or function blocks.                                                |
| `VAR_PERSISTENT`| Retained after PLC shutdown or restart.              | Values retained across power cycles.                                                                      |
| `VAR CONSTANT`  | As long as the program runs. Read-only.              | Values that shouldn't be modified after initialization.                                                   |
| `VAR_TEMP`      | Temporary during one invocation. Local accessibility.| Very short-lived temporary values.                                                                        |
| `VAR RETAIN`    | Retained across PLC restarts.                       | Values retained across restarts, but persistence across power loss might not be guaranteed.                |
| `VAR_ACCESS`    | Defined by accessibility properties.                 | Used in libraries where variable's access should be defined by the library user.                          |

