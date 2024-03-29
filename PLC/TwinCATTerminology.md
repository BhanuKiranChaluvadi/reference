# TwinCAT Terminology

Below is a table explaining various terms and abbreviations used in the TwinCAT development environment (`TcXaeShell`):

| Abbreviation   | Explanation                                                                                                 |
|----------------|-------------------------------------------------------------------------------------------------------------|
| DUT            | Data User Type - custom data types like structures or enumerations.                                          |
| FB             | Function Block - reusable code with an internal state.                                                       |
| FC             | Function - similar to FBs but without internal state.                                                        |
| GVLs           | Global Variable Lists - lists containing globally accessible variables.                                      |
| ITFs           | Interfaces - define a set of functions and methods to be implemented.                                        |
| N0_E01/N0_E02  | Likely specific variable or instance names; may be project-specific.                                         |
| POVs           | Process Object Variables (contextual; might not be a standard TwinCAT abbreviation).                         |
| POUsImplicits  | Program Organization Units Implicits - blocks of code like functions, FBs, or programs; "Implicits" may be default or automatically included units. |
| Sequence       | Refers to a sequence of operations or steps, like in sequence programming.                                  |
| VISUs          | Visualizations - graphical interfaces for interaction or monitoring.                                         |
|                |                                                                                                              |
| RTD            |  Resistance Temperature Detector (RTD)                                                                       |
| AI             | Analog input (AI) channel. EX: Configure analog input (AI) channel properties to measure temperature from a Resistance Temperature Detector (RTD). |

                                                                                    |


## PLC POUs vs. C++ Concepts

<table>
<tr>
<td>POU (PLC)</td>
<td>C++ Analogy</td>
<td>Description & C++ Example</td>
</tr>

<tr>
  <td>Program (PRG)</td>
  <td>`main()` function</td>
  <td>

  ```c++
  int main()
  {
    return 0;
  }
  ```

  </td>
</tr>

<tr>
  <td>Function (FC)</td>
  <td>Regular function</td>
  <td>

  ```c++
  int add(int a, int b)
  {
    return a + b;
  }
  ```

  </td>
</tr>

<tr>
  <td>Function Block (FB)</td>
  <td>Class</td>
  <td>

  ```c++
  class Counter
  {
  private:
    int count;

  public:
    Counter() : count(0) {}
    
    void increment()
    {
      count++;
    }

    int getCount()
    {
      return count;
    }
  };
  ```

  </td>
</tr>
</table>
