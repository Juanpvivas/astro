# Spec: Robot Instructor Canino "Astro"

## Descripción General

Astro es un robot de entrenamiento automatizado asistido por una cámara/coprocesador ESP32-CAM y sensores interactivos. El sistema guía a un perro llamado Oreo mediante comandos de voz pregrabados y valida el cumplimiento de las órdenes usando un sensor de proximidad y un sensor de presión. Si Oreo obedece dentro del tiempo límite de 2 minutos, recibe un premio de comida de forma automática; si falla, el robot emite un sonido de desaprobación.

---

## Historias de Usuario (El "Qué")

### Historia 1: Comando de Llamado y Proximidad
**Prioridad: 1 MVP**

**Como** Dueño de Oreo,
**Quiero** que Astro llame al perro por su nombre y detecte si se acerca usando un sensor de proximidad,
**Para** asegurar que Oreo asista al inicio de la sesión de entrenamiento antes de recibir su primer premio.

**Criterios de Aceptación (Cómo sabremos que funciona):**

- **Dado que** Astro inicia la sesión de entrenamiento, **Cuando** reproduce el audio pregrabado con el nombre "Oreo", **Entonces** se activa un temporizador de 2 minutos y el sistema empieza a leer el sensor de proximidad.
- **Dado que** el sensor de proximidad está activo, **Cuando** registra que Oreo se ha acercado con éxito dentro del límite de tiempo, **Entonces** Astro activa automáticamente el mecanismo para lanzarle un premio de comida, espera 2 minutos en reposo y avanza al siguiente comando.

---

### Historia 2: Comando de Habilidad "Rasca"
**Prioridad: 1 MVP**

**Como** Dueño de Oreo,
**Quiero** que Astro le ordene a Oreo rascar un área específica y valide la acción mediante un sensor de presión,
**Para** estimular las habilidades físicas y cognitivas del perro a cambio de una recompensa.

**Criterios de Aceptación:**

- **Dado que** pasaron los 2 minutos de descanso tras el primer premio, **Cuando** Astro reproduce el audio pregrabado "Rasca", **Entonces** se activa un nuevo temporizador de 2 minutos y el sistema monitorea el sensor de presión.
- **Dado que** el sensor de presión está activo, **Cuando** Oreo rasca con suficiente fuerza la superficie del sensor dentro de los 2 minutos, **Entonces** Astro le lanza automáticamente otro premio de comida y finaliza la sesión con éxito.

---

### Historia 3: Gestión de Fallos por Tiempo de Espera
**Prioridad: 1 MVP**

**Como** Dueño de Oreo,
**Quiero** que el robot emita una señal auditiva de error si Oreo no cumple la orden en el tiempo establecido,
**Para** indicarle auditivamente al perro que perdió la oportunidad de ganar el premio y cerrar el ciclo de manera ordenada.

**Criterios de Aceptación:**

- **Dado que** Astro emitió cualquiera de los dos comandos ("Oreo" o "Rasca"), **Cuando** el temporizador llega a los 2 minutos (Timeout) sin recibir la señal del sensor correspondiente (proximidad o presión), **Entonces** Astro debe reproducir un audio de fallo (un silbido o un "oh, qué mal"), NO lanza comida y finaliza el ciclo de entrenamiento.

---

## Casos Borde y Escenarios de Error

- ¿Qué pasa si Oreo se queda acostado presionando el sensor de presión antes de que Astro diga la palabra "Rasca"?
- ¿Qué pasa si el sensor de proximidad detecta un objeto inanimado o a otra persona en lugar de a Oreo?
- ¿Qué pasa si el dispensador se bloquea mecánicamente al intentar soltar una de las galletas?

---

## Requisitos Clave (Must-Haves)

- El sistema **DEBE** integrar un altavoz para reproducir de forma nítida los tres tipos de audio: comandos, éxitos y fallos.
- El sistema **DEBE** contar con un sensor de proximidad funcional y un sensor de presión operable por el perro.
- El contenedor físico de Astro **DEBE** tener una capacidad mínima para almacenar y dosificar 5 premios por sesión.
- El sistema **NO DEBE** despachar comida si el temporizador de 2 minutos expira antes de activar el sensor correspondiente.

---

## Criterios de Éxito (El "Por Qué")

Sabremos que esto es un éxito si Oreo completa de forma guiada y autónoma los dos comandos, recibiendo sus respectivas recompensas espaciadas por el intervalo de descanso.

El objetivo de negocio/personal es establecer una rutina interactiva de adiestramiento básico con hardware que proporcione retroalimentación clara tanto para el acierto como para el fallo.
