# BLDC Motor Controller

Controlador de motor BLDC (conmutación trapezoidal, sensores Hall) con lazo de 
control PID de velocidad y comunicación Modbus RTU. Diseño de placa de potencia 
propia en KiCad; firmware bare-metal en C sobre STM32F446RE (NUCLEO-F446RE).

## Estado actual
Fase 1 del roadmap de aprendizaje completada: GPIO por acceso directo a registros 
(sin HAL). El proyecto BLDC arranca en firme al completar Fase 3 (timers/PWM, 
ADC, UART).

## Estructura del repositorio
- `firmware/` — código fuente C, sin HAL
- `hardware/kicad/` — esquemático y PCB del driver
- `docs/decisions/` — justificación de decisiones de diseño relevantes
- `docs/debug-log.md` — registro de fallos encontrados y su resolución
- `test/logic-analyzer-captures/` — capturas de validación de señales
