# Decisión: sistema de build inicial

**Fecha:** 2026-08-18
**Estado:** Vigente, revisar en fase de toolchain avanzado

## Contexto
El proyecto usa STM32CubeIDE con managed build (Eclipse CDT). El Makefile 
real se genera automáticamente en `Debug/makefile` en cada compilación y 
no es apto para versionar: contiene rutas absolutas de la máquina local 
y se regenera en cada build.

## Decisión
No se versiona el Makefile autogenerado. `firmware/Makefile` queda como 
placeholder documentado hasta escribir un Makefile manual como ejercicio 
explícito del roadmap (toolchain: compilador → linker → objcopy → flash).

## Consecuencias
Cualquiera que clone el repo debe compilar por ahora usando STM32CubeIDE, 
no `make`. Se documentará el proceso de importación del proyecto en el 
README cuando se suba el `.ioc`/configuración necesaria.