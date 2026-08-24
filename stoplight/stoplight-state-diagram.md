```mermaid
stateDiagram-v2
    [*] --> Red 
    Red: Red / cars stop
    Red --> Green : timer ends
    Green: Green / cars go
    Green --> Yellow : timer ends
    Yellow: Yellow / cars slow down and stop
    Yellow --> Red : timer ends
```
