```mermaid
sequenceDiagram
    actor U as User
    participant CS as ChargingStation
    participant CH as ChargingSession
    participant C as Cable
    participant D as Display
    participant P as PaymentTerminal


    Note over U, P: Scenario 1: User charges until complete
    U->>C: connect()
    CS->>C: getState()
    C-->>CS: available
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: paymentMethod
    CS->>P: processPayment()
    P-->>CS: paymentResult
    alt paymentResult == success
        CS->>D: showPaymentSuccess()
        CS->>CH: startTime()
        CH-->>CS: ok
        CH->>CS: chargingComplete
        CS-->>CH: ok
        CS->>CH: endTime()
        CH-->>CS: ok
        U->>C: disconnect()
        C->>CS: cableDisconnected
        CS->>D: displaySessionSummary()
        D-->>CS: ok
    else paymentResult == failure
        CS->>D: showPaymentFailure()
    end

    Note over U, P: Scenario 2: User stops charging
    U->>C: connect()
    CS->>C: getState()
    C-->>CS: available
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: paymentMethod
    CS->>P: processPayment()
    P-->>CS: paymentResult
    alt paymentResult == success
        CS->>D: showPaymentSuccess()
        CS->>CH: startTime()
        CH-->>CS: ok
      alt charging stopped == button
            U->>CS: pressStopCharging()
            CS->>CH: endTime()
            CH-->>CS: ok
            U->>C: disconnect()
            C->>CS: cableDisconnected
      else charging stopped == cable disconnected
            U->>C: disconnect()
            C->>CS: cableDisconnected
            CS->>CH: endTime()
            CH-->>CS: ok
      end      
        CS->>D: displaySessionSummary()
        D-->>CS: ok
    else paymentResult == failure
        CS->>D: showPaymentFailure()
    end

    Note over U, P: Scenario 3a: Station Out of order
    U->>D: readDisplay()
    D-->>U: outOfOrder

    Note over U, P: Scenario 3b: Connection failed
    U->>C: connect()
    C->>CS: failed
    CS->>D: displayOutOfOrder()
    D-->>CS: ok
    U->>C: disconnect()
    C->>CS: cableDisconnected

    Note over U, P: Scenario 3c: Authentication failed
    U->>C: connect()
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: failed
    CS->>D: displayOutOfOrder()
    D-->>CS: ok
    U->>C: disconnect()
    C->>CS: cableDisconnected

    Note over U, P: Scenario 3d: Charging failed
    U->>C: connect()
    CS->>C: getState()
    C-->>CS: available
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: paymentMethod
    CS->>P: processPayment()
    P-->>CS: paymentResult
    alt paymentResult == success
        CS->>D: showPaymentSuccess()
        CS->>CH: startTime()
        CH-->>CS: ok
        CS->>CS: faultDetected
        CS->>CH: endTime()
        CH-->>CS: ok
        CS->>D: displayOutOfOrder()
        D-->>CS: ok
        U->>C: disconnect()
        C->>CS: cableDisconnected
    else paymentResult == failure
        CS->>D: showPaymentFailure()
    end

    Note over U, P: Scenario 3e: failed at charging complete
    U->>C: connect()
    CS->>C: getState()
    C-->>CS: available
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: paymentMethod
    CS->>P: processPayment()
    P-->>CS: paymentResult
    alt paymentResult == success
        CS->>D: showPaymentSuccess()
        CS->>CH: startTime()
        CH-->>CS: ok
        CH->>CS: chargingComplete
        CS-->>CH: ok
        CS->>CS: faultDetected
        CS->>CH: endTime()
        CH-->>CS: ok
        CS->>D: displayOutOfOrder()
        D-->>CS: ok
        U->>C: disconnect()
        C->>CS: cableDisconnected
    else paymentResult == failure
        CS->>D: showPaymentFailure()
    end

    Note over U, P: Scenario 3f: failed at stop charging
    U->>C: connect()
    CS->>C: getState()
    C-->>CS: available
    C->>CS: cableConnected
    CS->>P: getPaymentMethod()
    P-->>CS: paymentMethod
    CS->>P: processPayment()
    P-->>CS: paymentResult
    alt paymentResult == success
        CS->>D: showPaymentSuccess()
        CS->>CH: startTime()
        CH-->>CS: ok
      alt charging stopped == button
            U->>CS: pressStopCharging()
            CS->>CH: endTime()
            CH-->>CS: ok
            U->>C: disconnect()
            C->>CS: cableDisconnected
      else charging stopped == cable disconnected
            U->>C: disconnect()
            C->>CS: cableDisconnected
            CS->>CH: endTime()
            CH-->>CS: ok
      end     
        CS->>D: displaySessionSummary()
        D-->>CS: ok
        CS->>CS: faultDetected
        CS->>D: displayOutOfOrder()
        D-->>CS: ok
    else paymentResult == failure
        CS->>D: showPaymentFailure()
    end


    ```
    