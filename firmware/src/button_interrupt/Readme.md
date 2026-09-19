# Button Interrupt — Bare Metal STM32F446RE

## Descripción
Programa bare-metal que implementa una interrupción externa (EXTI). 
Al pulsar el botón B1 integrado en la placa, se ejecuta una ISR que 
invierte el estado del LED — sin necesidad de sondear el pin en el 
bucle principal.

## Hardware
Placa: NUCLEO-F446RE (STM32F446RE, ARM Cortex-M4, 180 MHz)

Pin: PA5 (Puerto A, pin 5 — LED2 integrado en la placa)  
Pin: PC13 (Puerto C, pin 13 — Botón B1 integrado en la placa)

## Registros configurados

### GPIO
- **RCC_AHB1ENR** (0x40023830): habilita los clocks de GPIOA (bit 0) 
  y GPIOC (bit 2).
- **GPIOA_MODER** (0x40020000): configura PA5 como salida digital 
  (bits 11:10 = 01).
- **GPIOA_ODR** (0x40020014): controla el estado lógico de PA5 — 
  invertido por la ISR con XOR.
- **GPIOC_PUPDR** (0x4002080C): activa la resistencia pull-up interna 
  en PC13 (bits 27:26 = 01), evitando que el pin quede flotante.

### EXTI
- **RCC_APB2ENR** (0x40023844): habilita el clock del SYSCFG (bit 14), 
  necesario antes de configurar la conexión de línea EXTI.
- **SYSCFG_EXTICR4** (0x40013814): conecta el puerto C a la línea 
  EXTI13 (bits 7:4 = 0010).
- **EXTI_FTSR** (0x40013C0C): habilita la detección de flanco de 
  bajada en la línea 13 — el pulsador conecta el pin a GND al pulsarse.
- **EXTI_IMR** (0x40013C00): desenmascara la línea EXTI13, permitiendo 
  que la señal llegue al NVIC.
- **EXTI_PR** (0x40013C14): registro de flag pendiente — se limpia al 
  final de la ISR para evitar que se repita en bucle.

### NVIC
- **NVIC_ISER1** (0xE000E104): habilita IRQ40 (bit 8), correspondiente 
  a las líneas EXTI10–EXTI15, autorizando al CPU a ejecutar la ISR.

## Compilación
STM32CubeIDE con toolchain arm-none-eabi-gcc.  
Proyecto tipo Empty — sin código HAL generado automáticamente.
