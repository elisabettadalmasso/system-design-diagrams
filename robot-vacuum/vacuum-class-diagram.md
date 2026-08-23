```mermaid
classDiagram
    class Vacuum {
        -brand: string
        -model: string
        -status: string
        -batteryLevel: number
        + powerOn()void
        + powerOff()void
        + clean()void
        + returnToBase()void
        + charge()void
        + alert() void
    }

    class Battery {
        -capacity: number
        -chargeRate: number
        -level: number
        -isCharging: boolean
        -health: string
        + charge()void
        + discharge()void
        +isCharged() boolean
        +isLow() boolean
        +getLevel() number
        +isFaulty() boolean
    }
    Vacuum *-- Battery

    class Brush {
        -type: string
        -size: number
        -material: string
        -shape: string
        +rotate() void
        +stop() void
        +isWorn() boolean
    }
    Vacuum "1" *-- "2" Brush

    class DockingStation {
        -location: string
        -isConnected: boolean
        -isOccupied: boolean
        -position: string
        +isOccupied() boolean
        +isConnected() boolean
        +isLocated() boolean
        +dock(Vacuum) void
        +undock(Vacuum) void
    }
    Vacuum o-- DockingStation

    class WheelMotor {
        -speed: number
        -running: boolean
        -direction: string
        +start() void
        +stop() void
        +isRunning() boolean
        +getSpeed() number
        +getDirection() string
        +setDirection(direction: string) void
    }
    Wheel *-- WheelMotor

    class BrushMotor {
        -running: boolean
        -direction: string
        +start() void
        +stop() void
        +isRunning() boolean
        +getDirection() string
    }
    Brush *-- BrushMotor

    class SuctionMotor {
        -running: boolean
        +start() void
        +stop() void
        +isRunning() boolean
    }
    Vacuum *-- SuctionMotor

    class Sensor {
        -type: string
        -isActive: boolean
        -obstacle: boolean
        +activate() void
        +deactivate() void
        +isActive() boolean
        +detectObstacle() boolean
    }
    Vacuum "1" *-- "4" Sensor

    class RemoteControl {
        -isConnected: boolean
        +connect() void
        +disconnect() void
        +isConnected() boolean
        
    }
    Vacuum o-- RemoteControl

    class Wheel {
        -size: number
        -material: string
        +rotate() void
        +stop() void
        
    }
    Vacuum "1" *-- "4" Wheel
```