```mermaid
stateDiagram-v2
    [*] --> Red 
    Red: Red / cars stop
    Red --> Green : timer stop
    Green: Green / cars go
    Green --> Yellow : timer stop
    Yellow: Yellow / cars slow down and stop
    Yellow --> Red : timer stop
```
