# Tasks: Robot Instructor Canino "Astro"

## Fase 1: Setup / Fundacional (Bloqueantes)

- [ ] **[Setup Hardware]** Realizar las conexiones físicas en el protoboard: conectar el sensor de proximidad (HC-SR04), el sensor de presión (FSR), el servomotor y el DFPlayer Mini a los pines correspondientes del Arduino Uno.

- [ ] **[Setup Audio]** Grabar o generar los tres archivos de audio con voz clara: 0001_oreo.mp3, 0002_rasca.mp3 y 0003_fallo.mp3. Guardarlos en una carpeta llamada MP3 dentro de la tarjeta MicroSD e insertarla en el DFPlayer Mini.

- [ ] **[Setup Software]** Crear la estructura de carpetas local /astro-robot, /astro_uno y /astro_esp32_cam en tu computador.

---

## Fase 2: Espejo de Video (ESP32-CAM)

- [ ] **[ESP32-CAM]** Crear el archivo astro_esp32_cam/astro_esp32_cam.ino.

- [ ] **[ESP32-CAM]** Configurar las credenciales de tu red Wi-Fi local (SSID y Contraseña) en el código.

- [ ] **[ESP32-CAM]** Implementar el código del servidor web para transmitir el streaming de la cámara en vivo y cargar el programa al módulo.

---

## Fase 3: Historia 1 - Comando "Oreo" y Proximidad (MVP)

- [ ] **[Arduino Backend]** Crear el archivo astro_uno/astro_uno.ino e inicializar las librerías para el Servomotor y el DFPlayer Mini.

- [ ] **[Arduino Backend]** Definir las variables de tiempo usando millis() para controlar el temporizador de 2 minutos de forma no bloqueante.

- [ ] **[Arduino Lógica]** Programar el Estado 1: Reproducir el audio 0001_oreo.mp3 al iniciar y comenzar a leer el sensor de proximidad en un bucle continuo.

- [ ] **[Arduino Actuadores]** Programar la rutina de éxito: Si el perro se acerca antes de los 2 minutos, accionar el servomotor para abrir y cerrar la compuerta del premio.

- [ ] **[Arduino Lógica]** Programar el temporizador de descanso: Bloquear el sistema en un estado de espera pasiva durante 2 minutos exactos después de entregar el primer premio.

---

## Fase 4: Historia 2 - Comando "Rasca" y Presión (MVP)

- [ ] **[Arduino Lógica]** Programar el Estado 2: Al terminar los 2 minutos de descanso, reproducir el audio 0002_rasca.mp3 e iniciar un nuevo temporizador de 2 minutos.

- [ ] **[Arduino Lógica]** Configurar la lectura del pin analógico del sensor de presión (FSR) estableciendo un umbral mínimo de fuerza para evitar falsos positivos.

- [ ] **[Arduino Actuadores]** Programar la rutina de éxito final: Si el sensor supera el umbral de presión dentro del tiempo estipulado, accionar el servomotor por segunda vez para lanzar comida.

---

## Fase 5: Historia 3 - Gestión de Fallos (Timeout)

- [ ] **[Arduino Lógica]** Programar la lógica de reincorporación por Timeout: Si en el Estado 1 o en el Estado 2 el contador de millis() supera los 2 minutos sin recibir señal de los sensores, cambiar el estado del robot a "Fallo".

- [ ] **[Arduino Actuadores]** Programar la rutina de fallo: Detener las lecturas de los sensores, reproducir el archivo de audio 0003_fallo.mp3, asegurar que el servomotor permanezca cerrado y finalizar la sesión de entrenamiento.
