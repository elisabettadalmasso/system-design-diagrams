```mermaid
stateDiagram-v2
    [*] --> Off
    Off : Off / display off
    Off --> On : power on
    On : On / system running
    On --> Off : power off
    On --> Off : power failure
    On --> maintenance : start maintenance
    maintenance : maintenance / service mode
    maintenance --> On : end maintenance
```
