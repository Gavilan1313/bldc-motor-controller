# LED Blink — Bare Metal STM32F446RE

## Descripción
Programa bare-metal que ejecuta un bucle infinito de encendido y apagado 
del LED integrado en intervalos de aproximadamente 0,5 segundos. 
Sin HAL — control directo de registros del hardware.

## Hardware
Placa: NUCLEO-F446RE (STM32F446RE, ARM Cortex-M4, 180 MHz)  
Pin: PA5 (Puerto A, pin 5 — LED2 integrado en la placa)

## Registros configurados
- **RCC_AHB1ENR** (0x40023830): habilita el clock del periférico GPIOA. 
  Sin este paso, cualquier escritura en los registros GPIO no tiene efecto.
- **GPIOA_MODER** (0x40020000): limpia los bits 11:10 con máscara y 
  configura PA5 como salida digital (valor 01 en bits 11:10).
- **GPIOA_ODR** (0x40020014): controla el estado lógico del pin — 
  alto o bajo. El bucle invierte el bit 5 con XOR para alternar el LED.

## Compilación
STM32CubeIDE con toolchain arm-none-eabi-gcc.  
Proyecto tipo Empty — sin código HAL generado automáticamente.
