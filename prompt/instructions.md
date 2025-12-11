## Design Principles

- **Avoid Tight Coupling**: Components should have minimal dependencies on specific implementations.
- **Testable & Simulatable**: Every component must support both real hardware and simulated behavior.
- **Simplicity & Optimization**: Follow KISS (Keep It Simple, Stupid), DRY (Don't Repeat Yourself), and YAGNI (You Aren't Gonna Need It) principles.
- **Single Responsibility**: Each class/module should have one clear purpose.
- **Separation of Concerns**: Business logic, hardware drivers, and application logic must remain independent.
- **Dependency Injection**: Push dependencies to clients rather than having them pull (Inversion of Control).
- **Behavior-Defined over Hardware-Defined**: Define software by what devices *do*, not what they *are*. This makes the codebase resilient to hardware changes and easier to maintain.
- **Hardware Abstraction**: Clients must interact through generic interfaces without needing to know specific hardware types or implementations.
