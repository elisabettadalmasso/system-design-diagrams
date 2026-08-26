```mermaid
stateDiagram-v2
    [*] --> Idle

    Idle : Idle / wait for charging request
    Idle --> Connected : cable connected
    Idle --> OutOfOrder : fault detected

    Connected : Connected / cable plugged, ready to authenticate
    Connected --> Authenticating : charging request received
    Connected --> Idle : cable disconnected
    Connected --> OutOfOrder : fault detected

    Authenticating : Authenticating / authenticate user, payment verification
    Authenticating --> Charging : payment verified
    Authenticating --> Idle : payment declined
    Authenticating --> OutOfOrder : fault detected

    Charging : Charging / charging the EV
    Charging --> ChargeComplete : battery full
    Charging --> Stopped : stop button pressed
    Charging --> Stopped : cable disconnected
    Charging --> OutOfOrder : fault detected

    ChargeComplete : ChargeComplete / display total cost
    ChargeComplete --> Idle : session closed
    ChargeComplete --> OutOfOrder : fault detected

    Stopped : Stopped / display total cost
    Stopped --> Idle : session closed
    Stopped --> OutOfOrder : fault detected

    OutOfOrder : OutOfOrder / display out of order
    OutOfOrder --> Idle : fault resolved
    ```
