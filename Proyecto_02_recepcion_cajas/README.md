# 📦 Sistema Automatizado de Clasificación Logística con RFID 

## 📋 Descripción del Proyecto
Este proyecto consiste en el diseño, programación y simulación de un **Gemelo Digital (Digital Twin)** para una planta logística de clasificación de paquetería. Desarrollado utilizando **Siemens TIA Portal** y **Factory I/O**, el sistema automatiza el enrutamiento de cajas hacia múltiples líneas de despacho basándose en la información leída por sensores RFID, integrando además un panel de control HMI para su operación.

El desarrollo se enfoca en resolver desafíos comunes de la automatización industrial, como la gestión de tiempos de ciclo (condiciones de carrera), la robustez de los sensores ante falsos rebotes y la manipulación segura de actuadores neumáticos.

## 🛠️ Tecnologías y Entorno
*   **PLC:** Siemens S7-1500 (CPU 1511-1 PN)
*   **Entorno de Desarrollo:** TIA Portal (STEP 7 Professional & WinCC)
*   **Simulador 3D:** Factory I/O (Comunicación vía S7-PLCSIM)
*   **Lenguajes de Programación:** Ladder Logic (KOP) y SCL (Structured Control Language).

## ⚙️ Características Técnicas y Soluciones Implementadas

*   **Programación Híbrida (Ladder + SCL):**
    *   Uso combinado de lenguajes gráficos para la lógica de enclavamientos secuenciales y texto estructurado (SCL) para optimizar el procesamiento de datos y la escalabilidad del código.
*   **Identificación y Enrutamiento Inteligente (RFID):**
    *   Procesamiento de datos provenientes de lectores RFID mediante bloques matemáticos (operaciones `MOD 10` y comparadores `==`) para extraer el código de destino de cada paquete y activar la secuencia correspondiente.
*   **Sincronización de Actuadores (Resolución de Race Conditions):**
    *   Implementación de temporizadores `TON` calibrados con precisión para sincronizar la lectura de datos del sensor difuso con el disparo de los empujadores neumáticos (Pushers), evitando fallos por la retención de memoria de cajas anteriores.
*   **Sistema de Conteo Robusto (Anti-Rebote):**
    *   Desarrollo de una lógica de conteo (`CTU`) vinculada a la confirmación física del actuador (Pusher) en lugar del sensor óptico. Esto elimina los "conteos fantasma" generados por la geometría de las cajas al caer o rebotar.
*   **Interfaz HMI y Control de Estados:**
    *   Panel WinCC integrado con botones de Marcha/Parada (Start/Stop).
    *   Lógica de retención de memoria para la parada del sistema: al presionar STOP, las fajas se detienen de forma segura sin perder la etapa actual de la secuencia, permitiendo reanudar el flujo exactamente donde se pausó.
