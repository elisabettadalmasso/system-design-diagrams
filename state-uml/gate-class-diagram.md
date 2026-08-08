```mermaid
classDiagram
    class Gate {
        -brand: string
        -model: string
        -state: string
        -lightOn: boolean
        -position: number
        +isOpen()boolean
        +open() void
        +isClosed() boolean
        +close() void
        +isStopped() boolean
        +stop() void
        +isMoving() boolean
        +alarm() void
    }

    class Motor {
        -type: string
        -speed: number
        -isRunning: boolean
        +run() void
        +stop() void
        +isRunning() boolean
    }
    Gate "1" *-- "1" Motor

    class Remote {
        -isConnected: boolean
        -batteryLevel: number
        +isConnected() boolean
        +getBatteryLevel() number
        +pressOpen() void
        +pressClose() void
        +pressStop() void
    }

    Gate "1" o-- "*" Remote

    class Sensor {
        -type: string
        -isActive: boolean
        +isActive() boolean
        +detectObstacle() boolean
    }

    Gate "1" *-- "2" Sensor

    class Timer {
        -duration: number
        -isRunning: boolean
        +start() void
        +stop() void
        +isRunning() boolean
        +isExpired() boolean
    }
    Gate "1" *-- "1" Timer.
  
  class Track {
        -material: string
        -length: number
        -isClean: boolean
  }
  Gate "1" o-- "1" Track

  class Wheel {
        -size: number
        -isSpinning: boolean
        +spin() void
        +stop() void
        +isSpinning() boolean
  }
  Gate "1" *-- "4" Wheel.
```