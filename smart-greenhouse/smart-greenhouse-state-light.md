```mermaid
stateDiagram-v2
    [*] --> Normal
    Normal : Normal / light level ok
    Normal --> High : light level too high
    High : High / close shade screen
    High --> Normal : light level ok
    Normal --> Low : light level too low
    Low : Low / open shade screen, turn on grow light
    Low --> Normal : light level ok
    High --> Error : shade screen failure
    Low --> Error : shade screen failure
    Low --> Error : grow light failure
    Error : Error / display error
    Error --> Normal : Problem resolved
```
