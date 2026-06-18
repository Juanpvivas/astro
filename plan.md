# Plan: Robot Instructor Canino "Astro"

## Spec de Referencia

Spec: Robot Instructor Canino "Astro" Final

---

## Contexto Técnico (Stack)

- **Microcontrolador Principal:** Arduino Uno (Lógica de estados, control de sensores y actuadores)
- **Coprocesador de Video:** Módulo ESP32-CAM
- **Lenguaje/Framework:** C++ (Arduino IDE) para ambos dispositivos
- **Componentes de Hardware:**
  - Sensor de Proximidad (ej. Ultrasónico HC-SR04)
  - Sensor de Presión (FSR - Force Sensing Resistor)
  - Servomotor (Control de la compuerta del dispensador de comida)
  - Módulo de Audio (DFPlayer Mini + Altavoz + Tarjeta MicroSD)

---

## Decisiones de Diseño Técnico

### 1. Centralización de Periféricos

El Arduino Uno leerá directamente el sensor de proximidad y el de presión, y controlará el servomotor y el DFPlayer Mini. Esto garantiza un tiempo de respuesta inmediato (sin latencia de red) cuando Oreo interactúe con los componentes físicos.

### 2. Rol de la ESP32-CAM

Funcionará de forma independiente como un servidor de streaming de video autónomo conectado a la red Wi-Fi local. Te permitirá monitorear visualmente el entrenamiento de Oreo desde un navegador web en tu celular o PC.

### 3. Máquina de Estados Basada en Tiempo

El código del Arduino Uno implementará una máquina de estados para gestionar el flujo secuencial del entrenamiento. Utilizará la función interna `millis()` para controlar el temporizador de 2 minutos (Timeout) y el descanso entre premios sin congelar el procesador.

### 4. Estructura de Almacenamiento de Audio

La tarjeta MicroSD del DFPlayer Mini contendrá exactamente tres archivos de audio organizados por índices fijos: `0001_oreo.mp3`, `0002_rasca.mp3` y `0003_fallo.mp3`.

---

## Estructura de Archivos Propuesta

El software se estructurará en dos firmwares independientes:

```
/astro-robot
│
├── /astro_uno
│   └── astro_uno.ino       <-- NUEVO: Controla la máquina de estados, lecturas de sensores, tiempos de 2 min y actuadores.
│
└── /astro_esp32_cam
    └── astro_esp32_cam.ino <-- NUEVO: Configura la cámara y el servidor web para el streaming de video por Wi-Fi.
```
